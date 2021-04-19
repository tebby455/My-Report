# Install LAMP Stack and LEMP Stack

**What is LAMP & LEMP**
**LAMP** and **LEMMP**based on

**L** stand for **Linux**
**A** stand for **Apache**, with **LEMP**, **E** stand for **Nginx**
**M** stand for **MySQL**, some system it uses **MariaDB**
**P** stand for **php**, some time nowadays it uses **perl**, **python**

- All of these combined into solution for web server more flexible.

## 1. LAMP Stack

a. **Apache2**
> apt-get install apache2 

b. **MySQL-Server**

![install Mysql Server](images/ubuntu/installMysql-server.png)

c. **Configure MySQL-Server**

![login](images/ubuntu/login.png)
> login to mysql

![change password](images/ubuntu/changepass.png)
> cahnge password for root, by default it is None

d. **Install Wordpress and setup**

![create database](images/ubuntu/createdatabase.png)
> Download wordpress

![download](images/ubuntu/wgetwp.png)

> then unzip this file

![setting](images/ubuntu/setting.png)
> Fill Database and Username database like in picture

![success](images/ubuntu/success.png)
> Login with your IP, DNS, in here I log in with _tebby455.info/wordpress
> Register username, password, then here is success to log in


![apache](images/ubuntu/apache.png)
> Check apache by `<?php phpinfo(); ?>`

## 2. LEMP Stack

![nginx](images/ubuntu/installNginx.png)
> _apt install php-fpm_ for support Nginx
> _service nginx start_ after installing

![config](images/ubuntu/configNginx.png)

![link config](images/ubuntu/link.png)
> link it into _/etc/nginx/sites-enabled/_

![check](images/ubuntu/ngin.png)
> Check php info again

![bingo](images/ubuntu/bingo.png)
> Success

***

# Advanced configure 

### 1. Reverse proxy for Nginx

> `cd /etc/nginx/conf.d`

> Create a new file, `nano domain.conf`

![configure Reverse Proxy](images/ubuntu/configReverse.png)

> Type these code into file **domain.conf**
> proxy_pass: set your ip, you want to direct to, in here I run two webserver _apache2_ and _nginx_, I use _nginx_ for reverse proxy to direct in _apache2_

> Restart nginx

![After Reversing](images/ubuntu/reverseDone.png)

### 2. Remote MySQL 

![show Database](images/ubuntu/showDatabase.png)

![create Remote Database](images/centos7/wordpress/createRemoteDatabase.png)
> I Created a new Database name: remoteddb


> Create an user in database with password is '123456a@'


> Allow access this user for all IP can connect: _grant all privileges on remotedb.* to 'user'@'%' with grant option;_
> _remotedb.*_ is allowed connect to database **remotedb**, if you allow all databases use `*.*`
> _'%'_ allowed for all IP can connect

![edit file Mysql](images/ubuntu/editFileSQL.png)
> add a comment to line _bind-address_

![connected](images/ubuntu/connected.png)
> Connect Successfully

### 3. **vsftpd**

![install vsftpd](images/ubuntu/installVSFTPD.png)

![set Port](images/ubuntu/allowPort.png)
> _ufw status_ to see all port allowed
> allow port: 20,21,22,40000:50000,990 and OpenSSH by command _ufw allow [port]_



![configure VSFTPD](images/ubuntu/configFTP.png)
> edit _listen=YES, listen_ipv6=NO_

![adding more Option](images/ubuntu/addConfig.png)
> Add these line in configure

![connected](images/ubuntu/connectedFTP.png)
> Connected

### 4. ***phpmyadmin***