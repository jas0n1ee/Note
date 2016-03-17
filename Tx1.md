#Nvidia Jetson Tx1

### Out of box
fix sshd wasn't install
```
sudo apt-get -y update && sudo apt-get install -y openssh-server vim  tmux git bash-completion 
sudo apt-get install yasm build-essential make cmake
```
## Installation

### Software

#### Linux For Tegra R23.2
[Overview](https://developer.nvidia.com/embedded/linux-tegra)
##### Download to HOST machine

```
wget http://developer.nvidia.com/embedded/dlc/l4t-jetson-tx1-driver-package-23-2 -O Tegra210_Linux_R23.2.0_armhf.tbz2
wget http://developer.nvidia.com/embedded/dlc/l4t-sample-root-filesystem-23-2 -O Tegra_Linux_Sample-Root-Filesystem_R23.2.0_armhf.tbz2
sudo tar xpf Tegra210_Linux_R23.2.0_armhf.tbz2
cd Linux_for_Tegra/rootfs/
sudo tar xpf ../../Tegra_Linux_Sample-Root-Filesystem_R23.2.0_armhf.tbz2
cd ../
sudo ./apply_binaries.sh
```
