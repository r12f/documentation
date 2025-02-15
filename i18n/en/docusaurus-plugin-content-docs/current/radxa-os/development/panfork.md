---
sidebar_position: 17
---

# RK3588 Installing Panfork Open Source GPU Driver

## Mainline Xorg server switching with Rockchip Xorg server

:::info
Although the official image comes with a vendor Mali driver, it only supports OpenGL ES, which is not compatible with the OpenGL interface used by most applications in the Linux ecosystem.  
The Panfork open source driver needs to run on the mainline Xorg server, and the vendor Mali driver needs to run on the Rockchip Xorg server.  
So we need the following command to switch the Xorg server version.
:::

```bash
sudo apt update
sudo apt-get install xserver-xorg-core/bullseye

#   To restore the Rockchip Xorg server, run the following command
#   sudo apt-get install  xserver-xorg-core/rockchip-bullseye
```

## Installation of compilation dependencies

```bash
sudo apt update
sudo apt install build-essential meson git python3-mako libexpat1-dev bison flex libwayland-egl-backend-dev libxext-dev libxfixes-dev libxcb-glx0-dev libxcb-shm0-dev libxcb-dri2-0-dev libxcb-dri3-dev libxcb-present-dev libxshmfence-dev libxxf86vm-dev libxrandr-dev zlib1g-dev pkg-config libwayland-* libdrm*
sudo pip3 install cmake ninja
```

## Compile and install dri2to3

```bash
git clone https://gitlab.com/panfork/dri2to3.git
mkdir dri2to3/build
cd dri2to3/build
meson setup
sudo ninja install
```

## Compile and install libdrm

```bash
cd ~/
git clone https://gitlab.freedesktop.org/mesa/drm
mkdir drm/build
cd drm/build
meson
sudo ninja install
```

## Compile and install Wayland protocols

```bash
cd ~/
git clone https://gitlab.freedesktop.org/wayland/wayland-protocols
mkdir wayland-protocols/build
cd wayland-protocols/build
git checkout 1.24
meson
sudo ninja install
```

## Compile and install Mesa

```bash
cd ~/
git clone https://gitlab.com/panfork/mesa.git
mkdir mesa/build
cd mesa/build
meson -Dgallium-drivers=panfrost -Dvulkan-drivers= -Dllvm=disabled --prefix=/opt/panfrost
sudo ninja install
```

## Setting the priority of Panfork dependencies

```bash
echo /opt/panfrost/lib/aarch64-linux-gnu | sudo tee /etc/ld.so.conf.d/0-panfrost.conf
sudo mv /etc/ld.so.conf.d/00-aarch64-mali.conf /etc/ld.so.conf.d/2-aarch64-mali.conf
sudo ldconfig
```

## test effect

### 1.Restart Window Manager

```bash
systemctl restart sddm.service
```

### 2.Login Desktop

### 3.Open the virtual terminal corresponding to the desktop environment and run the following command

:::info
The driver runs better under Wayland, use apt to install `plasma-workspace-wayland` and select the corresponding session in the SDDM login screen.
:::

```bash
sudo apt update
sudo apt install glmark-x11 #Install glmark-wayland if your desktop is running in a Wayland environment.
glmark2
```

![glmark2 running result](/img/general-tutorial/panfork/panfork.webp)
