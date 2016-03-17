# Ubuntu 14.04
## Basic enviroment
```
apt-get -y install vim yasm tmux htop
apt-get -y install build-essential python-pip
apt-get -y install apt-get install make cmake cmake-curses-gui libssl-dev libfdk-aac-dev
```
## Nvidia Reletive

### Login Loop
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
