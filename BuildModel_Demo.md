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
> change password for root, by default it is None

d. **Install Wordpress and setup**

![create database](images/ubuntu/createdatabase.png)
> Setup database, if you want to confifure to remote acces, use _'user'@'%'_ instead of _'user'@'localhost'_
> Add _with grant option;_ in the last of line _grant all privileges_


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

To Install `phpmyadmin`, we install these packages.

> apt-get install phpmyadmin php-mbstring php-gettext –y

> In _php_ version 7.0 to latest, php-gettext will be changed by _php-common_

> In apache2, while installing _phpmyadmin_ you can create database default by dkconfig-common
> Default database is _phpmyadmin_, password you set.

![success installing phpmyadmin](images/ubuntu/Successphpmyadmin.png)
> Symbolic links _/usr/share/phpmyadmin/ /var/www/html_ if you run not found.

> Run it _[your IP]/phpmyadmin_

![login phpmyadmin](images/ubuntu/loginphpmyadmin.png)

> login with your database and password

### 5. **Laravel** 

`apt install composer`

`apt install php libapache2-mod-php php-mbstring php-xmlrpc php-soap php-gd php-xml php-cli php-zip php-bcmath php-tokenizer php-json php-pear`

![download Laravel](images/ubuntu/downloadLaravel.png)

`composer create-project laravel/laravel {dirname}`

![laravel](images/ubuntu/laravel.png)


![set up database](images/ubuntu/databaseLravel.png)
> setup database for _laravel_, in here i setup for anyone can remote access to this.

![laravel configure](images/ubuntu/laravelconf.png)
> create a file _laravel.conf_ in _/etc/apache2/sites-available/laravel.conf_ then enanle it by `a2ensite laravel.conf`
> Or you can symbolic link _laravel.conf_

![configure env](images/centos7/wordpress/configEnv.png)
> Open file _/var/www/html/laravel/.env_ edit with your database

![before running](images/ubuntu/beforeRunning.png)
> Run command _php artisan serve --host=192.168.111.222 --port=8000_ before go to web.

![success](images/ubuntu/laravelRunning.png)
> Type _[IP]:port_

# Compiling and Installing from Source (Apache & Nginx)

### 1. Nginx

**Install PCRE**

> PCRE is a require module for the NGINX core and rewrite.

![download PCRE from source](images/ubuntu/Compile/nginx/downloadPCRE.png)
> Unzip it by _tar -xvzf [file]_

> locate to File then _./configure_

> make

> make install

**Install zlib**

> zlib - support header compression

![download zlib](images/ubuntu/Compile/nginx/downloadzlib.png)

> Unzip it by _tar -xvzf [file]_

> locate to file unziped then _./Configure_

> running **Make**

> **Make install**

**Install OpenSSL**

> OpenSSL supports the HTPS protocol

![download OpenSSL](images/ubuntu/Compile/nginx/downloadOpenSSL.png)

> Unzip it by _tar -xvzf [file]_

> locate to file unziped then _./Configure_

> running **Make**

> **Make install**

**Install Nginx**

> Download stable version of Nginx

`wget https://nginx.org/download/nginx-1.20.0.tar.gz`

> Unzip it `tar -xvzf [file]`

`mkdir  -p /web/nginx`
`mkdir /web/nginx/modules`
`mkdir  /web/nginx/run`

`./configure --prefix=/web/nginx --modules-path=/web/nginx/modules --with-http_ssl_module  --without-http_fastcgi_module --without-http_uwsgi_module --without-http_grpc_module --without-http_scgi_module --without-mail_imap_module --without-mail_pop3_module `

> Then make && make install

> locate to _/usr/local/nginx/sbin_ then _./nginx_ to start service

![start Nginx](images/ubuntu/Compile/nginx/startNginx.png)

### 2. Apache

**Install APR & APR-Util**

> This is Apache Portable Runtime is supporting library for the Apache webs server.

1. **APR**

> Download it from source: wget https://mirror.downloadvn.com/apache//apr/apr-1.7.0.tar.gz 

> After downloading, unzip it _tar -xvzf [file]_

Running `./configure --prefix=/usr/local/apr`

> running **Make**

> **Make install**

___

2. **APR-Utils**

> Download it from source: wget https://mirror.downloadvn.com/apache//apr/apr-util-1.6.1.tar.gz

> After downloading, unzip it _tar -xvzf [file]_

Running `./configure --prefix=/usr/local/apr-util --with-apr=/usr/local/apr/`

- If you running then has a problem with expat, do this:

    * Downloading from here: `wget https://github.com/libexpat/libexpat/releases/download/R_2_3_0/expat-2.3.0.tar.gz`
    * `./configure --prefix=/usr/local/expat`
    * `make`
    * `make install`

After this, running `./configure --prefix=/usr/local/apr-util --with-apr=/usr/local/apr/ --with-expat=/usr/local/expat/`

> **Make**

> **Make Install**

___

3. **Apache (httpd 2.4)**

> Download it from source: wget https://downloads.apache.org/httpd/httpd-2.4.46.tar.gz

> Unzip it `tar -xvzf [file]`

Running `./configure --prefix=/usr/local/apache2 --with-apr=/usr/local/apr/ --with-expat=/usr/local/expat/`

> **Make**

> **Make Install**

> Configure apache, because I install nginx and apache running dual, so I have to set port for each, default port of each is 80

`cd /usr/local/apache2/conf/httpd.conf`
![set Port](images/ubuntu/Compile/nginx/setPort.png)

![set Server](images/ubuntu/Compile/nginx/setServer.png)
> Edit ServerName by your IP if you dont have DNS, add a `#` to ServerAdmin


`cd /usr/local/apache2/bin`
`./apachectl start`

![start Apache](images/ubuntu/Compile/nginx/startApache.png
)

___

### 3. More Configuration

1. **Reverse Proxy**

![reverse Proxy](images/ubuntu/Compile/nginx/reverseProxy.png)

`cd /usr/local/nginx/conf/nginx.conf`

> Edit file configure like this, replace your server_name and proxy_pass

> When I access to nginx, reverse proxy direct me to apache

![reverse success](images/ubuntu/reverseDone.png)

2. **vsftpd**

![allow POrt](images/ubuntu/Compile/nginx/allowPort.png)

> Allow port

![configure vsftpd](images/ubuntu/Compile/nginx/configureVSFTPD.png)

![add User](images/ubuntu/Compile/nginx/addUser.png)

> After adding user, allow acces for it, `chown -R user:user [file]`

![success vsftpd](images/ubuntu/Compile/nginx/succesvsftpd.png)

> Connected

3. **mysql Remote Access**

![login](images/ubuntu/Compile/nginx/login_changepasswd.png)

> login and change password with 'root' user

![set up Database](images/ubuntu/Compile/nginx/setupDatabase.png)

> Create a user for remote access

![set Configure Database](images/ubuntu/Compile/nginx/editConfigDB.png)

> Add a `#` before line _bind-address_

![remote success](images/ubuntu/Compile/nginx/remoteSuccess.png)

> Remote successfully

4. **phpmyadmin**

- **Install php**

    * `wget https://www.php.net/distributions/php-8.0.3.tar.gz`
    * Unzip `tar -xvzf [file]`

    * To configure `/configure --with-apxs2=/usr/local/apache2/bin/apxs --with-mysqli --enable-mbstring --with-gettext`, while running if there are any missing packet, you can install with `apt-get`
    * Next `make` and `make install`

    ![add File Configure](images/ubuntu/Compile/nginx/addFileConfigure.png)

    > Edit like that

    * Restart apache, `/usr/local/apache2/bin/apachectl restart`
    * To check infophp, create a file `.php` with content `<? php\nphpinfo()?>` in directory `/usr/local/apache2/htdocs/`


- **Install phpmyadmin**

    * Run `apt-get install phpmyadmin`, while running it will require to setup a database with default name: phpmyadmin, password you set.
    * Symbolic links file `/etc/phpmyadmin/apache.conf` to `/usr/local/apache2/conf`, type `ln -s /etc/phpmyadmin/apache.conf /usr/local/apache2/conf`
    * Symbolic link `ln -s /usr/share/phpmyadmin /usr/local/apache2/htdocs/`, because apache2 will run any file in `htdocs`.

    ![seting file configure](images/ubuntu/Compile/nginx/configDatabase.png)

5. **Install Wordpress**

- **Set up database for Wordpress**

    ![setupdatabse wordpress](images/ubuntu/Compile/nginx/databaseWordPress.png)

    * `wget https://wordpress.org/latest.zip`
    * unzip it `unzip [file`]
    * move file after unzipping to `/usr/local/apache2/htdocs`
    * restart apache then run