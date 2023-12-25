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

