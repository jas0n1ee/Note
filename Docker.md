# Docker

## Installation

```sh
curl -fsSL https://get.docker.com/ | sh
```

## Quick Reference
### Set up docker proxy
For Ubuntu/Debian, edit `/etc/default/docker` and add a line like this:
`export http_proxy="http://your.proxy.server:80/"`
### Set up docker image directory
For Ubuntu/Debian, edit `/etc/default/docker` file with `-g` option, e.g:
`DOCKER_OPTS="-g /data/docker"`
## Nvidia Docker
[Official Repo](https://github.com/NVIDIA/nvidia-docker)  
Quick Cmd:
```sh
git clone https://github.com/NVIDIA/nvidia-docker
cd nvidia-docker
sudo make install
sudo nvidia-docker volume setup
```
