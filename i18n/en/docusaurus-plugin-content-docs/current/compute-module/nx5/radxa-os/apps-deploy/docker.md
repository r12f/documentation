---
sidebar_position: 1
---

# Docker

Radxa Debian already has Docker-related configuration enabled in the kernel, so you just need to install the Docker application to get started.

1. Install Docker

```
sudo apt-get update
sudo apt-get install docker.io
```

2. After the installation is complete, execute the following two commands

```
sudo update-alternatives --set iptables /usr/sbin/iptables-legacy
sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
sudo reboot
```

3. Run docker test after reboot and check the status.

```
sudo docker run hello-world
sudo systemctl status docker
```
