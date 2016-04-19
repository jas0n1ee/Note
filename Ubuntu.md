# Ubuntu 14.04

### Quick Links
- [Login Loop](#login-loop)
- [Static ip](#static-ip)
- [Correct date](#correct-date)

## Basic enviroment
```
apt-get -y install vim yasm tmux htop
apt-get -y install build-essential python-pip
apt-get -y install apt-get install make cmake cmake-curses-gui libssl-dev libfdk-aac-dev
```

### Login Loop 
after install/update nvidia driver
try backup and move `.Xauthority`
```
mv ~/.Xauthority ~/.Xauthority.backup
```
try reconfigure lightdm
```
sudo dpkg-reconfigure lightdm
```
try install something
```
sudo apt-get install linux-generic
```
try reinstall nvidia-display-driver

try reconfigure xserver-xorg
```
sudo dpkg-reconfigure xserver-xorg
```
### Static ip
```
#/etc/network/interfaces
auto eth0
iface eth0 inet static
address 0.0.0.0
netmask 255.255.255.0
gateway 0.0.0.0
dns-nameservers 8.8.8.8 
```

### Correct date

```bash
#set date
sudo date --set="STRING"
#check hardware current time
sudo hwclock -r
#if necessary, sync hardware to current time
sudo hwclock --systohc
```

