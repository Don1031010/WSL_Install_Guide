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

sudo service apache2 restart
```


