---
title: 通过Chevereto搭建私有图床 - ZH
tags: Image-hosting Linux Docker
---

# 前言

在长期使用的图床网站变更了它的域名后，我一时无法使用图床服务，虽然在后面又找到了它新的域名，但是还是觉得长期使用它并不是一个明智的决定。在考虑到安全与隐私，我使用了该图床网站同款工具也就是Chevereto进行私有图床的搭建，考虑到环境配置的复杂，在搭建过程中通过docker进行安装。

# 安装Docker

## 卸载旧版本

首先，如果有的话，先卸载旧版本

```bash
 sudo apt-get remove docker docker-engine docker.io containerd runc
```

## 设置仓库

在第一次安装Docker引擎之前，需要设置Docker仓库。

1. 先安装 apt 依赖包，用于通过HTTPS来获取仓库

   ```bash
    sudo apt-get update
    sudo apt-get install \
       apt-transport-https \
       ca-certificates \
       curl \
       gnupg \
       lsb-release
   ```

2. 添加官方 GPG 密钥

   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```

3. 设置为稳定版仓库

   ```bash
   echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

## 安装Docker Engine

1. 更新apt包索引，安装Docker Engine最新版本

   ```bash
   sudo apt-get update
   sudo apt-get install docker-ce docker-ce-cli containerd.io
   ```

2. 通过运行hello-world镜像，验证Docker Engine已正确安装，成功会打印欢迎信息

   ```bash
   sudo docker run hello-world
   ```

## 安装Docker-Compose

1. 下载当前稳定版的Docker-Compose

   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   ```

2.  将二进制文件设为可执行状态

   ```bash
   sudo chmod +x /usr/local/bin/docker-compose
   ```

3. 验证安装是否成功，成功会返回相应版本

   ```bash
   docker-compose --version
   ```

## 其他

当然，安装Docker的方式不止一种，还可以通过yum来安装Docker，这里不过多赘述。

```bash
yum install -y docker-latest
```

# 安装Chevereto

## 获取相关镜像

1. 给用户添加权限加入到docker组，或者给后面的步骤中命令加上sudo

   ```bash
   sudo gpasswd -a username docker   
   newgrp docker  
   ```

2. 安装Chevereto

   ```shell
   docker search chevereto
   docker pull nmtan/chevereto
   ```

3. 安装数据库，这里可以选择MySQL或MariaDB 

   ```shell
   docker search mariadb
   docker pull mariadb
   ```

   ```shell
   docker search mysql
   docker pull mysql
   ```

4. 验证是否成功

   ```shell
   docker images
   ```

## 配置Docker-Compose文件

1. 准备Chevereto工作目录

   ```bash
   mkdir chevereto
   cd chevereto
   touch docker-compose.yaml
   ```

2. 配置yaml文件

   ```yaml
   version: '3'
   
   services:
     db:
       image: mariadb
       volumes:
         - /chevereto/database:/var/lib/mysql:rw
       restart: always
       networks:
         - private
       environment:
         MYSQL_ROOT_PASSWORD: chevereto_root
         MYSQL_DATABASE: chevereto
         MYSQL_USER: chevereto
         MYSQL_PASSWORD: chevereto
   
     chevereto:
       depends_on:
         - db
       image: nmtan/chevereto
       restart: always
       networks:
         - private
       environment:
         CHEVERETO_DB_HOST: db
         CHEVERETO_DB_USERNAME: chevereto
         CHEVERETO_DB_PASSWORD: chevereto
         CHEVERETO_DB_NAME: chevereto
         CHEVERETO_DB_PREFIX: chv_
       volumes:
         - /chevereto/chevereto_images:/var/www/html/images:rw
       ports:
         - 8080:80
   
   networks:
     private:
   volumes:
     database:
     chevereto_images:
   ```

3. 启动容器

   ```shell
   docker-compose up -d
   ```

4. 查看是否启动成功

5. 为 images 文件夹添加权限

   ```shell
   chmod 777 /chevereto/chevereto_images
   ```

------

**Reference/参考**: 

1. [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
2. [Install Docker Compose](https://docs.docker.com/compose/install/)
3. [Chevereto V3 Docs](https://v3-docs.chevereto.com/)
4. [安装指南](https://docs.doge.uk/zh/chevereto/v3/contributed.html#%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97)



