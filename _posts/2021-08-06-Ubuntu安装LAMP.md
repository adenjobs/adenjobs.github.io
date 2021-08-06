---
layout: post
title:  "Ubuntu安装LAMP"
date:   2021-08-06 13:30:00 +0800
categories: ubuntu lamp
tags:
    - ubuntu
    - lamp
    - php7.2
---

# Ubuntu安装LAMP

## PHP7.2
```
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get install php7.2
```

## Apache2
```
sudo apt-get install apache2
```

## PHP常用扩展
```
sudo apt-get install php7.2-fpm php7.2-mysql php7.2-curl php7.2-json php7.2-mbstring php7.2-xml  php7.2-intl 
```
## 其他扩展
```
sudo apt-get install php7.2-gd
sudo apt-get install php7.2-soap
sudo apt-get install php7.2-gmp    
sudo apt-get install php7.2-odbc       
sudo apt-get install php7.2-pspell     
sudo apt-get install php7.2-bcmath   
sudo apt-get install php7.2-enchant    
sudo apt-get install php7.2-imap       
sudo apt-get install php7.2-ldap       
sudo apt-get install php7.2-opcache
sudo apt-get install php7.2-readline   
sudo apt-get install php7.2-sqlite3    
sudo apt-get install php7.2-xmlrpc
sudo apt-get install php7.2-bz2
sudo apt-get install php7.2-interbase
sudo apt-get install php7.2-pgsql      
sudo apt-get install php7.2-recode     
sudo apt-get install php7.2-sybase     
sudo apt-get install php7.2-xsl
sudo apt-get install php7.2-cgi        
sudo apt-get install php7.2-dba 
sudo apt-get install php7.2-phpdbg     
sudo apt-get install php7.2-snmp       
sudo apt-get install php7.2-tidy       
sudo apt-get install php7.2-zip
```

## Mysql
```
sudo apt-get install mysql-server
sudo apt install mysql-client
sudo apt install libmysqlclient-dev
```

### Mysql更新密码
```
mysql> use mysql;

// mysql 5.7
mysql> update user set authentication_string=PASSWORD("密码") where user='root';
 
// mysql8 以上
mysql> ALTER USER '你的用户名默认root'@'localhost' IDENTIFIED WITH mysql_native_password BY '你的密码';

mysql> update user set plugin="mysql_native_password";

mysql> flush privileges;

mysql> exit;
// 重启mysql服务
service mysql restart

```

### Mysql创建UTF-8数据库
```
CREATE DATABASE `mydb` CHARACTER SET utf8 COLLATE utf8_general_ci;
```