# Goal
The goal of this project to make setting up a D.O. box efficient and repeatable.

The result should be a server that fulfills all its basic functions and is relatively secure.

# Usage
To create a site, run `sudo mksite example.com`

To completely wipe a site from the server, run `sudo wipesite example.com`

# Building the Box
## Droplet Setup
  - Create a new **LAMP on 16.04** droplet through digitalocean.com
  - Connect via SSH: `root@ip_address`
  - Run through initial setup as per [this article][1]
  - Run `mysql_secure_installation`
  - [Create a server mysql user][2]:
    ```mysql
    CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
    GRANT ALL PRIVILEGES ON * . * TO 'user'@'localhost';
    FLUSH PRIVILEGES;
    ```
  - Log out of `root`

[1]: https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04
[2]: https://www.digitalocean.com/community/tutorials/how-to-create-a-new-user-and-grant-permissions-in-mysql

## User Setup
  - Log in as the `serveruser` created above
  - Run `$ sudo visudo` and add `serveruser ALL = NOPASSWD : ALL` so that running `sudo` commands does not require a password.

## Installations
### essentials
    cd
    sudo apt-get update
    sudo apt-get install build-essential
    sudo apt-get install zip
    sudo apt-get install unzip

### git
    sudo apt-get install git

### PHP extensions
    sudo apt-get install php-curl php-gd php-mbstring php-mcrypt php-xml php-xmlrpc

### certbot
    sudo ufw allow 443
    sudo add-apt-repository ppa:certbot/certbot

    sudo apt-get install python-certbot-apache

    sudo crontab -e

Put this in that file: `15 3 * * * /usr/bin/certbot renew --quiet`

### ruby
    sudo apt install ruby

### linuxbrew
    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install)"

    PATH="/home/linuxbrew/.linuxbrew/bin:$PATH"
    echo 'export PATH="/home/linuxbrew/.linuxbrew/bin:$PATH"' >>~/.profile

### yarn (also installs node, so win/win)
    brew install yarn

### composer
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
    php -r "if (hash_file('SHA384', 'composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
    php composer-setup.php
    php -r "unlink('composer-setup.php');"

### /home/user/bin
    sudo git clone https://github.com/ethanbeyer/DigitalOcean-Droplet-Setup.git
    sudo chmod +x ~/bin/*

## Installation Cleanup
    sudo apt-get dist-upgrade
    sudo-apt-get update
    sudo a2enmod rewrite
    sudo apache2ctl configtest
    sudo systemctl restart apache2
