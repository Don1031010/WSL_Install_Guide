# WSL_Install_Guide

## Install Apache

Install follow [artical on DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-22-04)
Skip `ufw` setting.

```sh
sudo apt update
sudo apt install apache2

sudo service apache2 start
```

Open http://localhost using browser and confirm apache2 is running.

* root directory is `/var/www/html/`
* configuration files at `/etc/apache2/`
* `apache2.conf` is the main configuration file. It puts the pieces together by including all remaining configuration files when starting up the web server.

## Installing MySQL

```sh
sudo apt install mysql-server

sudo service mysql start
sudo mysql
```

### setting password for root@localhost

Add following to `/etc/mysql/mysql.cnf`.

```sh
[mysqld]
skip-grant-tables
```

```sh
sudo mysql

flush privileges;
use mysql;
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
```

Restore `mysql.cnf` and restart mysql.


## Installing PHP 8.3

Following php.watch's artical [How to install or upgrade to PHP 8.3 on Ubuntu and Debian](https://php.watch/articles/php-8.3-install-upgrade-on-debian-ubuntu#php83-ubuntu-quick)
```sh
# Add Ondrej's PPA
sudo add-apt-repository ppa:ondrej/php # Press enter when prompted.
sudo apt update

# Install new PHP 8.3 packages
sudo apt install php8.3 php8.3-cli php8.3-{bz2,curl,mbstring,intl}

# Install FPM OR Apache module
sudo apt install php8.3-fpm

# On Apache: Enable PHP 8.3 FPM
sudo a2enconf php8.3-fpm

# install php curl and xml extensions
sudo apt install php8.3-curl
sudp apt install php8.3-xml

sudo service apache2 restart
```

## Install Composer

Download instructions at [getcomposer.org](https://getcomposer.org/download/)

```sh
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'e21205b207c3ff031906575712edab6f13eb0b361f2085f1f1237b7126d785e826a450292b6cfd1d64d92e6563bbde02') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```
Move and rename `composer.phar` to `~/.local/bin/composer` (create ~/.local directory if not exists).

## Installing Node with nvm

Github [instructions](https://github.com/nvm-sh/nvm)

```sh
nvm install --lts
node -v  # v20.10.0
npm -v   # 10.2.3
```

## Installing phpMyAdmin

```sh
sudo apt install phpmyadmin
```

This doesn't work. Switch to HeidiSQL for client.

Change Mysql `auth_plugin` to `mysql_native_password@ and set root password.
```sh
sudo mysql
use mysql;
select user, host, plugin from user; # should show | root | localhost | auth_socket |

# from auth_socket to mysql_native_password
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

select user, host, plugin from user; # should show | root | localhost | mysql_native_password |
```

## ssh-keygen

run `ssh-keygen` and set up github ssh key.

## set default php version to 8.3

```sh
sudo update-alternatives --set php /usr/bin/php8.3

ls -l /usr/bin/php*
php -v
```

## install php8.3-mysql

```sh
php -m | grep mysql
sudo apt install php8.3-mysql

sudo service apache2 restart
sudo service mysql restart
```


