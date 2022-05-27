# Install LAMP in WSL2

## Install Debian in WSL2

- Run PowerShell as Administrator:

```
wsl --install -d Debian
```

## Upgrade Debian from Buster to Bullseye

- In the Debian shell:

```
sudo apt update && sudo apt upgrade -y
```

- Check the version of your distro:

```
cat /etc/debian_version
```

- Modify the sources:

```
sudo nano /etc/apt/sources.list
```

- Delete all the content of the file, and past this:

```
deb http://deb.debian.org/debian bullseye main
deb http://deb.debian.org/debian bullseye-updates main
deb http://security.debian.org/debian-security/ bullseye-security main
```

> Press `CTRL` + `O` for overwriting, confirm by pressing `Enter`, and leave nano by pressing `CTRL` + `X`.

```
sudo apt update && sudo apt upgrade -y
```

- Upgrade the version:

```
sudo apt full-upgrade -y
```

> Select `yes` when needed.

```
sudo apt autoremove -y
```

- Check that the version is up to date:

```
cat /etc/debian_version
```

- Install additional packages:
```
sudo apt install -y software-properties-common curl wget openssh-server
```

## [optional] No Password

```
sudo nano /etc/sudoers
```

- At the last line of the file, paste:

```
# NO PASSWORD
%sudo   ALL=(ALL:ALL) NOPASSWD:ALL
```

## Install MariaDB

```
sudo apt install -y mariadb-server
```

```
mysql --version
```

```
sudo service mariadb start
```

```
sudo mysql_secure_installation
```

```
NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!
In order to log into MariaDB to secure it, we'll need the current
password for the root user. If you've just installed MariaDB, and
haven't set the root password yet, you should just press enter here.
Enter current password for root (enter for none):
OK, successfully used password, moving on...
Setting the root password or using the unix_socket ensures that nobody
can log into the MariaDB root user without the proper authorisation.
You already have your root account protected, so you can safely answer 'n'.
Switch to unix_socket authentication [Y/n] y
Enabled successfully!
Reloading privilege tables..
 ... Success!
You already have your root account protected, so you can safely answer 'n'.
Change the root password? [Y/n] y
New password:
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
 ... Success!
By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.
Remove anonymous users? [Y/n] y
 ... Success!
Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.
Disallow root login remotely? [Y/n] y
 ... Success!
By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.
Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!
Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.
Reload privilege tables now? [Y/n] y
 ... Success!
Cleaning up...
All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.
Thanks for using MariaDB!
```

```
sudo mysql -u root -p
```
- Change *username* and *password*:

```
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost';
EXIT
```

## Install Apache

```
sudo apt install -y apache2
```

```
sudo service apache2 start
```

```
sudo nano /etc/apache2/sites-enabled/000-default.conf
```

- Change ```DocumentRoot /var/www/html``` to ```DocumentRoot /var/www```.

- Change permissions:

```
sudo chgrp $(id -u) -R /var/www && sudo chown www-data -R /var/www && sudo chmod 775 -R /var/www
```

## Install Node.js

```curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash```

- Close the Debian shell and restart it.

```command -v nvm```

- If returns `nvm`, it works !

```
nvm install --lts
```

```
nvm install node
```

## Install PHP

```
sudo apt -y install lsb-release apt-transport-https ca-certificates 
```

```
sudo curl -sSL -o /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
```

```
sudo sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
```

```
sudo apt update && sudo apt -y upgrade && sudo apt -y autoremove
```

```
sudo apt -y install php8.0 libapache2-mod-php8.0 php8.0-{bcmath,bz2,intl,gd,mbstring,mysql,zip,curl,dom}
```

```
sudo service apache2 restart
```

### PHP errors

```
sudo nano /etc/php/8.0/apache2/php.ini
```

- Change the default value of `error_reporting` from `E_ALL & ~E_NOTICE & ~E_STRICT & ~E_DEPRECATED` to `E_ALL`:

```
error_reporting = E_ALL
```

- Change the default value of `display_errors` from `Off` to `On`:

```
display_errors = On
```

- View error logs when you debug your code in PHP::

```
cat /var/log/apache2/error.log
```

### Install Postfix

```
sudo apt install -y postfix
```

- Choose `Internet Site` then keep the default values.

```
sudo nano /etc/postfix/main.cf
```

- Change value of `then keep the default values` to `127.0.0.1:1025`.

### Install MailDev

```
npm install -g maildev
```

- Start MailDev: 

```
maildev --ip 127.0.0.1
```

- In the URL bar of your browser, type:

```
http://127.0.0.1:1080
```

- Close MailDev by pressing `CTRL` + `C`.


## Install Adminer

```
sudo apt install -y adminer
```

```
sudo a2enconf adminer
```

```
sudo service apache2 restart
```

- In the URL bar of your browser, type: 

```
localhost/adminer
```

## Install GIT

```
sudo apt install git -y
```

- Change *your-username* and *your-mail@example.com*:

```
git config --global user.name your-username
git config --global user.email your-mail@example.com
```

- You can change this information at any time:

```
sudo nano ~/.gitconfig
```

### Authenticate with SSH key on GitHub

- Create GitHub account: [Join GitHub](https://github.com/join)

- Generate your SSH Key: 

```
ssh-keygen -t rsa -b 2048
```

- Display your SSH Key and copy it:

```
cat ~/.ssh/id_rsa.pub
```

- Then paste it into GitHub.

## Install VSCode 

- Download and install [Visual Studio Code](https://code.visualstudio.com/Download)

- Install [Remote - WSL](https://aka.ms/vscode-remote/download/wsl)

## Init

```
sudo nano ~/.bashrc
```

- At the last line of the file, paste:

```
# Start apache2, mariadb & postfix
sudo service apache2 start && sudo service mariadb start && sudo service postfix start

# Start VSCode (Remote WSL)
code /var/www

# Start MailDev
maildev --ip 127.0.0.1
```


## Resources

- [Official Microsoft Documentation](https://docs.microsoft.com/fr-fr/windows/wsl/install)
- [WSL2 Guide for Debian](https://gist.github.com/xnebulr/c769f26bffd41db2667d1f9de9f8ce5a)

## Tools
- [Debian](https://www.debian.org/)
- [MariaDB Foundation](https://mariadb.org/)
- [The Apache Software Foundation](https://apache.org/)
- [PHP](https://www.php.net/)
- [The Postfix Home Page](http://www.postfix.org/)
- [MailDev](https://maildev.github.io/maildev/)
- [Adminer](https://www.adminer.org/)
- [git](https://git-scm.com/)
- [GitHub](https://github.com/)
- [Visual Studio Code](https://code.visualstudio.com/)
