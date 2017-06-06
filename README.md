# DigitalOcean-Droplet-Setup

## Droplet Setup

1. Create a new droplet: LAMP on 16.04
2. If created with an SSH key, no password will be emailed.
3. Connect via SSH as root

## Initial Server Configuration

1. Follow through with [this article](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04)
2. Run `mysql_secure_installation`
3. [Create a server mysql user](https://www.digitalocean.com/community/tutorials/how-to-create-a-new-user-and-grant-permissions-in-mysql)
4. Log out as `root`

## Fine-grained Server Configuration

1. Log in as the user created in step 4
2. Disable all sites: `sudo a2dissite ...`
3. Add `user ALL = NOPASSWD : ALL` to `$ sudo visudo`
4. Connect via FTP, add this repo to `/home/user`



## All the server dependencies.

- **essentials**
```
sudo apt-get install build-essential
```

- **certbot**
```
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
```

```
sudo apt-get install python-certbot-apache
```

- **ruby**
```
sudo apt install ruby
```

- **linuxbrew**
```    
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install)"
```

```
PATH="/home/linuxbrew/.linuxbrew/bin:$PATH"
echo 'export PATH="/home/linuxbrew/.linuxbrew/bin:$PATH"' >>~/.bash_profile
```

- **npm**
```
brew install node
```

- **yarn**
```
brew install yarn
```

- **composer**
```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```