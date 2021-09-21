---
title: Crawl the Hearthston Card Data - EN
tags: Crawler
---

# Background

I played Hearthstone for a long time during the summer, and had the idea that I could do a deck strength analysis or win rate prediction or something like that, so I started with the Hearthstone dataset and got a lot of interesting Hearthstone-related products in the process of searching.

1. A neural network targeting code generation for mixed natural language and structured text is proposed in DeepMind's [Latent Predictor Networks for Code Generation](https://arxiv.org/abs/1603.06744) based on the Hearthstone and Magic datasets, the specific The dataset is visible at [card2code](https://github.com/deepmind/card2code).
2. The source of the dataset for the above paper is [Hearthbreaker](https://github.com/danielyule/hearthbreaker), a Hearthstone simulator project for machine learning and data mining.
3. The actual card data in the above project comes from [Hearthstone JSON](http://hearthstonejson.com/), a website that organizes card data into json format.
4. The above website is affiliated with [HearthSim](https://hearthsim.info/), and their [Github community](https://github.com/HearthSim) contributes useful projects such as a notetaker above.

The HearthstoneJSON log is only updated as of 2018-06-27, and its [project address](https://github.com/HearthSim/HearthstoneJSON) seems to be no longer maintained, fortunately two synchronized update interfaces based on the [cardsDefs.xml](https://github.com/HearthSim/hsdata) ([cards.json](https://api.hearthstonejson.com/v1/latest/enUS/cards.json) and [cards.collectible.json](https:// api.hearthstonejson.com/v1/latest/enUS/cards.collectible.json)) in [documentation](https://hearthstonejson. com/docs/cards.html) are still available.

In fact only cards.collectible.json is useful, because the other one actually contains all the content of Hearthstone and not the cards in the collection. Specific examples are as follows:

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

Thanks to HearthSim for the api, but what is more interesting is how they get this data, is there a way to get more concise data? Yes, the first reaction is definitely to go to the official website and use a crawler to get the filtered data, which is also a good example for me to learn about web scraping.

Go to Blizzard's Hearthstone official website https://playhearthstone.com/en-us and select Cards/Card Library to come to https://playhearthstone.com/en-us/cards. The two choices in the view mean different targets for crawling, namely card information and art resources. After the preparation work, let's begin.

# Analyze the Web Page

We first select TableView and choose Standard Cards, All Types in the filter. The web page will display the results sorted by mana cost and type, as shown below:

[![4lO4Qs.jpg](https://z3.ax1x.com/2021/09/18/4lO4Qs.jpg)](https://imgtu.com/i/4lO4Qs)

Open F12 and review the elements:

[![43kvYd.jpg](https://z3.ax1x.com/2021/09/19/43kvYd.jpg)](https://imgtu.com/i/43kvYd)

[![43Al0U.jpg](https://z3.ax1x.com/2021/09/19/43Al0U.jpg)](https://imgtu.com/i/43Al0U)

Then take a look at the packet capture:

[![4lO2FS.jpg](https://z3.ax1x.com/2021/09/18/4lO2FS.jpg)](https://imgtu.com/i/4lO2FS)

Find the request that respond to json data:

[![4lO6df.jpg](https://z3.ax1x.com/2021/09/18/4lO6df.jpg)](https://imgtu.com/i/4lO6df)

[![4lOqFU.jpg](https://z3.ax1x.com/2021/09/18/4lOqFU.jpg)](https://imgtu.com/i/4lOqFU)

We can directly read the card data:

[![4lOLYF.jpg](https://z3.ax1x.com/2021/09/18/4lOLYF.jpg)](https://imgtu.com/i/4lOLYF)

It specifically includes spells, minion, etc., and belongs to the Collectible type.

# Web Scraping

If we want to get the features of Card Name, Class, Mana, Attack, Health, Card Type, Rarity, Keywords, we can do a web scraping.

The first thought is to use Request + BeautifulSoup, which is a common combination. However, although the html displayed in the element review has tbody, tr, td tags, the content returned by the server does not have these tags. It is because the data on this website is obtained through the official api. Tags like tbody is the chrome rendering results. 

Considering that this is a dynamic web page that requires scroll down for loading to get the rest of the card data, perhaps using the powerful selenium would be a more appropriate choice.

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

Since the page is lazy loading, I have to drag the scrollbar to the bottom in order to get all the data. But the actual execution of the code for the scrollbar has no effect (maybe there is something wrong with my code), so I locate the element instead.

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

We can get the data including several features of Card Name, Mana, Attack, Health, Card Type, Rarity, and Keywords in the following form.

```
['Sigil of Silence/0/-/-/Spell - Shadow/Rare/Silence', 
'Battlefiend/1/1/2/Minion - Demon/Common/-']
```

Unfortunately I was not able to extract the Classes because it is strange that the page only uses icons to represent the Classes.

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

After several attempts, I gave up. This also meant that the data I obtained missed important features and did not meet the actual requirements.  Another way is to select a category and then crawl it, for example, choose https://playhearthstone.com/en-us/cards?class=demonhunter&set=standard&viewMode=table, at this time there is only Demon Hunter's cards.

# Get JSON Data through API

If we need to get official and more comprehensive card data, [Blizzard's official API](https://develop.battle.net/documentation/hearthstone) is a better choice, and it will also be easier to get data directly from the official data source.

Note that the page is a dynamic page, you can see that there are 980 cards in cardCount and 5 pages in pageCount, which means that the page loads 200 cards at a time and refreshes the next page when it is pulled down. We can make changes on the page when we specify the URL. Also for the Hearthstone official website, which uses Blizzard's API for requests, authorization is needed to add in the header.

```
Request URL: https://api.blizzard.com/hearthstone/cards?class=all&order=asc&pageSize=200&set=standard&sort=manaCost%3Aasc%2Cname%3Aasc%2Cclasses%3Aasc%2CgroupByClass%3Aasc&viewMode=table&locale=en_US
```

Let‘s do it:

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

We can get following data：

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

If you need to specify features, you can use `get` to get them, or get them via JsonPath.

------

Disclaimer: The data is Copyright © Blizzard Entertainment - All Rights Reserved

Please follow https://playhearthstone.com/robots.txt.

------

**Reference/参考**: 

1. [HearthstoneJSON](https://hearthstonejson.com/)
2. [selenium](https://www.selenium.dev/documentation/)



