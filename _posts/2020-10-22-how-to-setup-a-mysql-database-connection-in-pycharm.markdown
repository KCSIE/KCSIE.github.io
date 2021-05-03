---
title:  How to Setup a MySQL Database Connection in Pycharm
tags: MySQL Pycharm Database Tools
---

# Preparation

## Enter

+ Find the download path of MySQL (under the bin folder)

+ Open the CMD and jump to that path

+ Enter 

  ```
  MySQL -u root -p
  ```

   and your password for the root account to access the root account 

![1](https://s1.ax1x.com/2020/10/05/0Ygijg.jpg)

## Create a new account

+ Enter 

  ```
  CREATE USER 'Bob'@'localhost' IDENTIFIED BY '123456';
  ```

  It means that you have created an account with the username Bob, logged in locally, and the password is 123456

+ Next, don't log out from the root account. We need to authorize the new account. Enter 

  ```
  GRANT ALL ON *.* TO 'Bob'@'localhost';
  ```

  You authorize the local account with the username Bob to perform all operations on all databases and tables

+ Now you can enter 

  ```
  exit
  ```

   to leave

![2](https://s1.ax1x.com/2020/10/05/0Yfqw4.jpg)

# 准备工作

## 进入

+ 找到MySQL的下载路径 (bin文件夹下)

+ 打开CMD并跳转至相应路径

+ 输入

  ```
  MySQL -u root -p
  ```

  和你的root账户的密码来进入root账户

![3](https://s1.ax1x.com/2020/10/05/0Ygijg.jpg)

## 创建新账户

+ 输入

  ```
  CREATE USER 'Bob'@'localhost' IDENTIFIED BY '123456';
  ```

  这意味着你创建了一个用户名为Bob密码为123456的本地用户

+ 接着，不要退出当前的root账户。我们需要为新创建的账户授权。输入 

  ```
  GRANT ALL ON *.* TO 'Bob'@'localhost';
  ```

  你授权用户名为bob的本地账户可以对所有数据库和表的所有操作

+ 现在你可以输入

  ```
  exit
  ```

   来退出了

![4](https://s1.ax1x.com/2020/10/05/0Yfqw4.jpg)

# Connection

## Step1

Click the Database button on the right-hand side. Then click the Plus button to find the MySQL option in Data Source.

![5](https://s1.ax1x.com/2020/10/05/0Y4TZF.jpg)

## Step2

You will find this window.

![6](https://s1.ax1x.com/2020/10/05/0Y5fFH.jpg)

Now, we can get back to the MySQL to create a database.

Enter 

```
MySQL -h localhost -u Bob -p
```

and the password 123456 to enter this account.

Enter 

```
CREATE DATABASE warehouse;
```

which means you will create a database called warehouse.

After that, let's get back to Pycharm but don't exit MySQL because maybe you will use it later.

## Step3

Fill in the blanks in Pycharm.

![7](https://s1.ax1x.com/2020/10/05/0YIIN4.jpg)

Afterwards, click the Test Connection button.

![8](https://s1.ax1x.com/2020/10/05/0Yot54.jpg)

If you see a green tick, congrats! Click OK, done!

If not, don't worry, let's go on.

## Step4

The problem I met is 

```
The specified database user/password combination is rejected: [42000][1044]
```

It's caused by the invalid timezone. So I have to set ‘serverTimezone’ property.

Get back to the MySQL. Enter 

```
show variables like'%time_zone';
```

If your timezone is like this

![9](https://s1.ax1x.com/2020/10/05/0YT7Ox.png)

which means you have not set the timezone.

Thus, you need to enter 

```
set global time_zone = '+8:00';
```

to set it. ('+8:00' is my timezone, just set it up according to your location)

And then re-enter the account, you will find that the timezone has been changed.

![10](https://s1.ax1x.com/2020/10/05/0YHcIU.jpg)

Finally, return to Pycharm and click the Test Connection button again.

Likewise, if you see a green tick, then you succeed!

# 连接

## 第1步

点击右侧的Database按钮。然后点击加号按钮并在Data Source中寻找MySQL选项

![11](https://s1.ax1x.com/2020/10/05/0Y4TZF.jpg)

## 第2步

你会看到这个窗口。

![12](https://s1.ax1x.com/2020/10/05/0Y5fFH.jpg)

现在我们回到MySQL去创建数据库。

输入

```
MySQL -h localhost -u Bob -p
```

和密码123456进入Bob这个账号。

输入

```
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

```
The specified database user/password combination is rejected: [42000][1044]
```

它是由无效的时区造成的。所以我们需要正确的设置时区。

回到MySQL。输入 

```
show variables like'%time_zone';
```

如果你的时区是这样的

![15](https://s1.ax1x.com/2020/10/05/0YT7Ox.png)

这意味着你的时区还是默认的。

所以，你需要输入

```
set global time_zone = '+8:00';
```

来设置它。('+8:00' 是我的时区，根据你所在位置来设置时区吧)

然后重新进入该账户，你会发现时区已经被改变。

![16](https://s1.ax1x.com/2020/10/05/0YHcIU.jpg)

最后回到Pycharm并再次点击Test Connection按钮。

同样的，如果你看到绿色勾，你就成功了！



<img style="display: block; margin: 0 auto;" src="" alt="" />