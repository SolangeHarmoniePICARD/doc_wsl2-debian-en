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

