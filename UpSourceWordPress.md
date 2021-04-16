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