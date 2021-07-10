---
title:  如何在Pycharm中连接MySQL数据库 - ZH
tags: MySQL Pycharm Database Tools
---

# 准备工作

## 进入

+ 找到MySQL的下载路径 (bin文件夹下)

+ 打开CMD并跳转至相应路径

+ 输入

  ```sql
  MySQL -u root -p
  ```

  和你的root账户的密码来进入root账户

![3](https://s1.ax1x.com/2020/10/05/0Ygijg.jpg)

## 创建新账户

+ 输入

  ```sql
  CREATE USER 'Bob'@'localhost' IDENTIFIED BY '123456';
  ```

  这意味着你创建了一个用户名为Bob密码为123456的本地用户

+ 接着，不要退出当前的root账户。我们需要为新创建的账户授权。输入 

  ```sql
  GRANT ALL ON *.* TO 'Bob'@'localhost';
  ```

  你授权用户名为bob的本地账户可以对所有数据库和表的所有操作

+ 现在你可以输入

  ```sql
  exit
  ```

   来退出了

![4](https://s1.ax1x.com/2020/10/05/0Yfqw4.jpg)



# 连接

## 第1步

点击右侧的Database按钮。然后点击加号按钮并在Data Source中寻找MySQL选项

![11](https://s1.ax1x.com/2020/10/05/0Y4TZF.jpg)

## 第2步

你会看到这个窗口。

![12](https://s1.ax1x.com/2020/10/05/0Y5fFH.jpg)

现在我们回到MySQL去创建数据库。

输入

```sql
MySQL -h localhost -u Bob -p
```

和密码123456进入Bob这个账号。

输入

```sql
CREATE DATABASE warehouse;
```

这意味着你新创建了一个叫warehouse的数据库。

随后我们回到Pycharm，但别退出MySQL因为我们后面可能会用到它

## 第3步

填写Pycharm窗口里的空。

![13](https://s1.ax1x.com/2020/10/05/0YIIN4.jpg)

然后点击Test Connection按钮

![14](https://s1.ax1x.com/2020/10/05/0Yot54.jpg)

如果你看到绿色的勾，恭喜你! 点击OK，完成了！

如果没有，别担心，我们继续。

## 第4步

我遇到了这个问题

```sql
The specified database user/password combination is rejected: [42000][1044]
```

它是由无效的时区造成的。所以我们需要正确的设置时区。

回到MySQL。输入 

```sql
show variables like'%time_zone';
```

如果你的时区是这样的

![15](https://s1.ax1x.com/2020/10/05/0YT7Ox.png)

这意味着你的时区还是默认的。

所以，你需要输入

```sql
set global time_zone = '+8:00';
```

来设置它。('+8:00' 是我的时区，根据你所在位置来设置时区吧)

然后重新进入该账户，你会发现时区已经被改变。

![16](https://s1.ax1x.com/2020/10/05/0YHcIU.jpg)

最后回到Pycharm并再次点击Test Connection按钮。

同样的，如果你看到绿色勾，你就成功了！



<img style="display: block; margin: 0 auto;" src="" alt="" />