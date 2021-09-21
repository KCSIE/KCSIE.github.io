---
title: 爬取炉石卡牌数据 - ZH
tags: Crawler
---

# 背景

暑假玩了挺久炉石，突发奇想可不可以做个卡组强度分析或胜率预测啥的，先从炉石数据集开始找，在进行检索的过程中获取了许多炉石相关的有意思的衍生品。

1. DeepMind的[Latent Predictor Networks for Code Generation](https://arxiv.org/abs/1603.06744)一文中基于炉石和万智牌数据集提出了针对混合自然语言和结构化文本的代码生成的神经网络，具体的数据集在[card2code](https://github.com/deepmind/card2code)可见。
2. 上面的论文的数据集的来源是[Hearthbreaker](https://github.com/danielyule/hearthbreaker)这个针对机器学习和数据挖掘的炉石模拟器项目。
3. 上述项目中实际的卡牌数据则来自[Hearthstone JSON](http://hearthstonejson.com/)，这是一个将卡牌数据整理为json格式的网站。
4. 上述网站由隶属于[HearthSim](https://hearthsim.info/)，它们的[Github社区](https://github.com/HearthSim)上面包括记牌器等实用项目。

HearthstoneJSON日志只更新到2018-06-27，其[项目地址](https://github.com/HearthSim/HearthstoneJSON)似乎已经挂了，幸运的是其[文档](https://hearthstonejson.com/docs/cards.html)中([cards.json](https://api.hearthstonejson.com/v1/latest/enUS/cards.json), [cards.collectible.json](https://api.hearthstonejson.com/v1/latest/enUS/cards.collectible.json))两个基于[CardDefs.xml](https://github.com/HearthSim/hsdata)的同步更新接口都还在。实际上真正需要的是cards.collectible.json，因为另一个实际上包含了炉石传说的所有内容而不是收藏中的卡牌，具体实例如下：

```json
# Spell
{
 "artist":"Nutthapon Petchthai",
 "cardClass":"MAGE",
 "collectible":true,
 "cost":5,
 "dbfId":2539,
 "flavor":"It's on the rack next to ice lance, acid lance, and English muffin lance.",
 "id":"AT_001",
 "name":"Flame Lance",
 "rarity":"COMMON",
 "set":"TGT",
 "spellSchool":"FIRE",
 "text":"Deal $8 damage to a minion.",
 "type":"SPELL"
}
# Minion
{ 
 "artist":"Slawomir Maniak",
 "attack":2,
 "cardClass":"NEUTRAL",
 "collectible":true,
 "cost":4,
 "dbfId":2569,
 "flavor":"A result of magical experiments carried out by the Black Dragonflight, it's not his fault that he's a vicious killer.",
 "health":6,
 "id":"AT_017",
 "mechanics":["BATTLECRY"],
 "name":"Twilight Guardian",
 "race":"DRAGON",
 "rarity":"EPIC",
 "referencedTags":["TAUNT"],
 "set":"TGT",
 "text":"<b>Battlecry:</b> If you're holding a Dragon, gain +1 Attack and <b>Taunt</b>.",
 "type":"MINION"
}
```

感谢HearthSim提供的api，不过更令人感兴趣的是他们是如何获取这些数据的，有没有办法获取更简洁的数据？没错，第一反应肯定的是去官网用爬虫去获取筛选后的数据，这对我来说也是一个很好的学习爬虫并实践的例子。

进入暴雪炉石官网https://playhearthstone.com/en-us，选择Cards/Card Library来到https://playhearthstone.com/en-us/cards，在视图中的两种选择意味着爬取目标的不同，分别是卡牌信息和卡牌资源。做完了准备工作，下面便正式开始。

# 分析网页

我们先选择TableView，在过滤器中选择标准卡牌、所有类型，网页会根据费用、类型来排序显示结果，如下图所示：

[![4lO4Qs.jpg](https://z3.ax1x.com/2021/09/18/4lO4Qs.jpg)](https://imgtu.com/i/4lO4Qs)

打开F12，看看网页的元素构成：

[![43kvYd.jpg](https://z3.ax1x.com/2021/09/19/43kvYd.jpg)](https://imgtu.com/i/43kvYd)

[![43Al0U.jpg](https://z3.ax1x.com/2021/09/19/43Al0U.jpg)](https://imgtu.com/i/43Al0U)

然后看看抓包：

[![4lO2FS.jpg](https://z3.ax1x.com/2021/09/18/4lO2FS.jpg)](https://imgtu.com/i/4lO2FS)

找到响应json数据的请求：

[![4lO6df.jpg](https://z3.ax1x.com/2021/09/18/4lO6df.jpg)](https://imgtu.com/i/4lO6df)

[![4lOqFU.jpg](https://z3.ax1x.com/2021/09/18/4lOqFU.jpg)](https://imgtu.com/i/4lOqFU)

我们可以直观的看到该请求的信息，同时我们看看卡牌数据：

[![4lOLYF.jpg](https://z3.ax1x.com/2021/09/18/4lOLYF.jpg)](https://imgtu.com/i/4lOLYF)

具体的也包括法术、随从等，属于Collectible类型。

# 简单爬取

如果想获得Card Name、Class、Mana、Attack、Health、Card Type、Rarity、Keywords这几项特征，我们可以进行对网页的简单爬取。

首先想到就是使用Request+BeautifulSoup这个常用组合，然而在尝试时发现尽管在元素审查中显示的html具备tbody、tr、td标签，服务器返回的内容却没有这些标签，这是因为实际上炉石官网是通过api的链接获取的数据，tbody等则是是chrome渲染后的结果。考虑到这是个动态网页，需要下拉加载才能得到剩下的卡牌数据，或许用强大的selenium是更合适的选择。

```python
# for online notebook
!pip install selenium
!apt-get update
!apt install chromium-chromedriver
```

```python
import sys, time
from selenium import webdriver

options = webdriver.ChromeOptions()
options.add_argument('--headless')
options.add_argument('--no-sandbox')
options.add_argument('--disable-dev-shm-usage')
driver = webdriver.Chrome('chromedriver',options=options)
```

```python
url = 'https://playhearthstone.com/en-us/cards?set=standard&viewMode=table'

driver.get(url)
driver.set_window_size(1519.20,721.20)
driver.refresh()
```

由于该网页是懒加载，为了获取全部数据，我们要把滚动条拖至底部。但是实际执行滚动条的代码时没有效果，于是采用定位元素的方式。

```python
# handle the lazy loading, get the whole page
for i in range(5):
  target = driver.find_element_by_class_name('CardGridLayout__VisibilityPixel-sc-1xsi1ca-4')
  driver.execute_script("arguments[0].scrollIntoView();", target)
  time.sleep(5)
```

```python
basic_info = driver.find_elements_by_class_name('CardTableLayout__Row-sc-1jy3g9y-3')  

list = []

for i in basic_info:
  card = i.text.replace("\n", "/")
  list.append(card)

print(list)
```

我们可以得到包括Card Name、Mana、Attack、Health、Card Type、Rarity、Keywords几项特征的数据，形式如下。

```
['Sigil of Silence/0/-/-/Spell - Shadow/Rare/Silence', 
'Battlefiend/1/1/2/Minion - Demon/Common/-']
```

遗憾的是我无法将Class提取出来，因为很奇怪网页只采用了图标表示类别。

```
<td class="classes">
  <div class="CardTableLayout__TextWithIcon-sc-1jy3g9y-12 fswQmU">
    <div class="ClassIconContainer" id="tooltipItem_card-59026-druidIcon">
      <div class="CircleIcon-sc-1i97tg1-0 ClassIcon-sc-1haasd4-0 ClassControl__ItemIcon-sc-1bt92vh-1 fTCBLn ClassIcon DualClassIcon druid">
      </div>
    </div>
    <div class="ClassIconContainer" id="tooltipItem_card-59026-hunterIcon">
      <div class="CircleIcon-sc-1i97tg1-0 ClassIcon-sc-1haasd4-0 ClassControl__ItemIcon-sc-1bt92vh-1 fTCBLn ClassIcon DualClassIcon hunter">
      </div>
    </div>
  </div>
</td>
```

在经过许久尝试后，我放弃了，但这也意味着我获取的数据缺失了重要特征，不符合实际需求。另一种思路是选定分类后进行爬取，比如选择https://playhearthstone.com/en-us/cards?class=demonhunter&set=standard&viewMode=table，此时只有恶魔猎手一类卡牌。

# 通过API获取JSON数据

如果我们需要获取官方的更全面的卡牌数据，[暴雪官方的API](https://develop.battle.net/documentation/hearthstone)是更好的选择，直接从官方的数据源获取数据也会更简单方便。

需要注意的是该页面是动态网页，可以看到cardCount有980张，pageCount有5页，也就是说页面一次加载200张牌，当下拉时刷新下页。我们在规定URL时，可以在page上进行修改。同时对于炉石官网，使用了暴雪的API进行请求，需要授权，要在header中添加。

```
Request URL: https://api.blizzard.com/hearthstone/cards?class=all&order=asc&pageSize=200&set=standard&sort=manaCost%3Aasc%2Cname%3Aasc%2Cclasses%3Aasc%2CgroupByClass%3Aasc&viewMode=table&locale=en_US
```

下面进行获取：

```python
import requests
import json

base_url = 'https://api.blizzard.com/hearthstone/cards?class=all&order=asc&page={}&pageSize=200&set=standard&sort=manaCost%3Aasc%2Cname%3Aasc%2Cclasses%3Aasc%2CgroupByClass%3Aasc&viewMode=table&locale=en_US'
headers = {
    'Authorization':'Bearer KR0TZFpUeCM5q4QdrFqKfgdRUk5Wgayl4M',
    'Origin':'https://playhearthstone.com',
    'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.82 Safari/537.36'
}
pageCount = 5
```

```python
def get_url_list():
  return [base_url.format(i) for i in range(1,pageCount+1)]
  
def parse_url(url):
  print(url)
  resp = requests.get(url, headers = headers)
  jsonstr = resp.content.decode()
  json_data = json.loads(jsonstr) # turn str to dict
  return json_data
```

```python
url_list = get_url_list()

merge_list = []

for i in url_list:
  result = parse_url(i)
  data = result.get("cards") # dict to list, get data in "cards":[]
  print(data)
  for x in data:
    merge_list.append(x)

print(merge_list) #all data
```

可以得到如下形式的结果：

```json
[{
	"id": 63467,
	"collectible": 1,
	"slug": "63467-sigil-of-silence",
	"classId": 14,
	"multiClassIds": [],
	"spellSchoolId": 6,
	"cardTypeId": 5,
	"cardSetId": 1525,
	"rarityId": 3,
	"artistName": "Vlad Botos",
	"manaCost": 0,
	"name": "Sigil of Silence",
	"text": "At the start of your next turn, <b>Silence</b> all enemy minions.",
	"image": "https://d15f34w2p8l1cc.cloudfront.net/hearthstone/86b0f1dafbafcd88a036278e3e7a3657694e1790ea50281fa1fea760b19c80b0.png", 
	"imageGold": "",
	"flavorText": "A little heard-of spell.",
	"cropImage": "https://d15f34w2p8l1cc.cloudfront.net/hearthstone/fe448a4ba398df4a0f8d0fb26b1412bef0415d9c5a048ad250c6051566decfdb.png",
	"keywordIds": [15],
	"duels": {
		"relevant": true,
		"constructed": true
	}
}, {
	"id": 69586,
	"collectible": 1,
	"slug": "69586-battlefiend",
	"classId": 14,
	"multiClassIds": [],
	"minionTypeId": 15,
	"cardTypeId": 4,
	"cardSetId": 1637,
	"rarityId": 1,
	"artistName": "Andrew Hou",
	"health": 2,
	"attack": 1,
	"manaCost": 1,
	"name": "Battlefiend",
	"text": "After your hero attacks, gain +1 Attack.",
	"image": "https://d15f34w2p8l1cc.cloudfront.net/hearthstone/89fbd74fb6eeb96b470604f40a94d7439dd9079fc741ef6cb35bad07d8bdaff9.png",
	"imageGold": "",
	"flavorText": "Say what you like about my hatchet-headed hooligan, he’s my battle-friend.",
	"cropImage": "https://d15f34w2p8l1cc.cloudfront.net/hearthstone/465fca2734fdbc0e5039098359bf8e1cdcf35935754bc4949c4d4b9ff773db6f.png",
	"copyOfCardId": 58487,
	"duels": {
		"relevant": true,
		"constructed": true
	}
}]
```

如果需要指定特征，则可以使用get进行获取，或者通过JsonPath进行获取。

------

声明：所有数据版权归暴雪娱乐有限公司所有。

请遵循：https://playhearthstone.com/robots.txt.

------

**Reference/参考**: 

1. [HearthstoneJSON](https://hearthstonejson.com/)
2. [selenium](https://www.selenium.dev/documentation/)



