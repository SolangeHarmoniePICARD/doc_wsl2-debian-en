# Install LAMP in WSL2

## Install Debian in WSL2

- Run PowerShell as Administrator:

```
wsl --install -d Debian
```

## Upgrade Debian from Buster to Bullseye

- In the Debian terminal:

```
sudo apt update && sudo apt upgrade -y
```

```
sudo nano /etc/apt/sources.list
```

```
deb http://deb.debian.org/debian bullseye main
deb http://deb.debian.org/debian bullseye-updates main
deb http://security.debian.org/debian-security/ bullseye-security main
```

```
sudo apt update && sudo apt upgrade -y
```

```
sudo apt full-upgrade -y
```

```
sudo apt autoremove -y
```

```
cat /etc/debian_version
```

```
sudo apt install -y software-properties-common curl wget openssh-server
```

## [optional] No Password

```
sudo nano /etc/sudoers
```

- At the last line of the file:

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
- Change "username" and "password":

```
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost';
EXIT
```

