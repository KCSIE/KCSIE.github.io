---
title: 通过Chevereto搭建私有图床 - EN
tags: Image-hosting Linux Docker
---

# Preface

After the long-used image bed website changed its domain name, I couldn't use the image bed service for a while, although I found its new domain name later, but I still think it's not a wise decision to use it for a long time. Considering the security and privacy, I used the same tool of the image bed website, that is, Chevereto, to build a private image bed. Considering the complexity of the environment configuration, I installed it through docker during the building process.

# Install Docker

## Uninstall older versions

First, uninstall the old version if you have one.

```bash
 sudo apt-get remove docker docker-engine docker.io containerd runc
```

## Set up the repository

Before installing the Docker engine for the first time, you need to set up the Docker repository.

1. Update the apt package index and install packages to allow apt to use a repository over HTTPS.

   ```bash
    sudo apt-get update
    sudo apt-get install \
       apt-transport-https \
       ca-certificates \
       curl \
       gnupg \
       lsb-release
   ```

2. Add Docker’s official GPG key.

   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```

3. Set up the stable repository.

   ```bash
   echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

## Install Docker Engine

1. Update the apt package index and install the latest version of Docker Engine

   ```bash
   sudo apt-get update
   sudo apt-get install docker-ce docker-ce-cli containerd.io
   ```

2. Verify that if Docker Engine is installed correctly by running the hello-world image, a welcome message will be printed if successful.

   ```bash
   sudo docker run hello-world
   ```

## Install Docker-Compose

1. Download the current stable version of Docker-Compose.

   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   ```

2.  Apply executable permissions to the binary.

   ```bash
   sudo chmod +x /usr/local/bin/docker-compose
   ```

3. Check if the installation is successful, if it is, the corresponding version will be returned.

   ```bash
   docker-compose --version
   ```

## Other

Of course, there is more than one way to install Docker, and you can also install Docker via yum, I won't go into details here.

```bash
yum install -y docker-latest
```

# Install Chevereto

## Get related images

1. Add permissions to the user to join the docker group, or add `sudo` to the commands in the next steps.

   ```bash
   sudo gpasswd -a username docker   
   newgrp docker  
   ```

2. Install Chevereto.

   ```shell
   docker search chevereto
   docker pull nmtan/chevereto
   ```

3. Install the database, here you can choose MySQL or MariaDB.

   ```shell
   docker search mariadb
   docker pull mariadb
   ```

   ```shell
   docker search mysql
   docker pull mysql
   ```

4. Verify.

   ```shell
   docker images
   ```

## Configure the Docker-Compose file

1. Preparing the Chevereto working directory.

   ```bash
   mkdir chevereto
   cd chevereto
   touch docker-compose.yaml
   ```

2. Configuring yaml files.

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

3. Launching the container.

   ```shell
   docker-compose up -d
   ```

4. Check if the startup was successful.

5. Add permissions to the images folder

   ```shell
   chmod 777 /chevereto/chevereto_images
   ```

**Reference/参考**: 

1. [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
2. [Install Docker Compose](https://docs.docker.com/compose/install/)
3. [Chevereto V3 Docs](https://v3-docs.chevereto.com/)
4. [安装指南](https://docs.doge.uk/zh/chevereto/v3/contributed.html#%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97)



