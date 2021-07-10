---
title:  How to Setup a MySQL Database Connection in Pycharm - EN
tags: MySQL Pycharm Database Tools
---

# Preparation

## Enter

+ Find the download path of MySQL (under the bin folder)

+ Open the CMD and jump to that path

+ Enter 

  ```sql
  MySQL -u root -p
  ```

   and your password for the root account to access the root account 

![1](https://s1.ax1x.com/2020/10/05/0Ygijg.jpg)

## Create a new account

+ Enter 

  ```sql
  CREATE USER 'Bob'@'localhost' IDENTIFIED BY '123456';
  ```

  It means that you have created an account with the username Bob, logged in locally, and the password is 123456

+ Next, don't log out from the root account. We need to authorize the new account. Enter 

  ```sql
  GRANT ALL ON *.* TO 'Bob'@'localhost';
  ```

  You authorize the local account with the username Bob to perform all operations on all databases and tables

+ Now you can enter 

  ```sql
  exit
  ```

   to leave

![2](https://s1.ax1x.com/2020/10/05/0Yfqw4.jpg)



# Connection

## Step1

Click the Database button on the right-hand side. Then click the Plus button to find the MySQL option in Data Source.

![5](https://s1.ax1x.com/2020/10/05/0Y4TZF.jpg)

## Step2

You will find this window.

![6](https://s1.ax1x.com/2020/10/05/0Y5fFH.jpg)

Now, we can get back to the MySQL to create a database.

Enter 

```sql
MySQL -h localhost -u Bob -p
```

and the password 123456 to enter this account.

Enter 

```sql
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

```sql
The specified database user/password combination is rejected: [42000][1044]
```

It's caused by the invalid timezone. So I have to set ‘serverTimezone’ property.

Get back to the MySQL. Enter 

```sql
show variables like'%time_zone';
```

If your timezone is like this

![9](https://s1.ax1x.com/2020/10/05/0YT7Ox.png)

which means you have not set the timezone.

Thus, you need to enter 

```sql
set global time_zone = '+8:00';
```

to set it. ('+8:00' is my timezone, just set it up according to your location)

And then re-enter the account, you will find that the timezone has been changed.

![10](https://s1.ax1x.com/2020/10/05/0YHcIU.jpg)

Finally, return to Pycharm and click the Test Connection button again.

Likewise, if you see a green tick, then you succeed!





<img style="display: block; margin: 0 auto;" src="" alt="" />