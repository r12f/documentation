---
sidebar_position: 2
---

# 系统使用

主要介绍 Radxa OS 系统的基本使用方法，帮助你快速了解常用的系统的配置。

## 用户名和密码

Radxa ROCK 系列默认添加的用户名和密码为：

```
用户名：radxa/rock
密码：  radxa/rock
```

## 串口登录

Radxa ROCK 系列均配备 40PIN 排针接口，在40 PIN 排针接口上默认开启了系统串口调试。

:::tip
默认的串口调试波特率为 `1500000n8，无流量控制`,请确保使用的 USB 转 TTL 串口线支持 1.5M 波特率
:::

![USB to TTL](/img/accessories/600px-Usb2ttl-cable-definition.webp)

- 接线方法

如下所示连接 USB 转 TTL 串口线：

| Radxa SBC       | 连接  | 串口线 |
| --------------- | ----- | ------ |
| **GND** (pin 6) | <---> | 黑色线 |
| **TX** (pin 8)  | <---> | 白色线 |
| **RX** (pin 10) | <---> | 绿色线 |

![USB to TTL connected](/img/accessories/1000px-Serial-connection.webp)

- 使用 [Mobaxterm](https://mobaxterm.mobatek.net/) 调试串口

点击左上角的 `Session` 新建 Serial 连接，在 `Serial port` 处选择串口号， `Speed` 处填入 `1500000`, 点击 OK 后双击会话，输入密码后即可访问。

![mobaxterm serial ](/img/zero/zero3w/mobaxterm-serial.webp)

## 设置网络

### 连接WiFi

### 以太网连接

## 自动登录

为了更快进入桌面，可以设置桌面自动登录,修改 `/etc/lightdm/lightdm.conf` 文件

```
sudo vim /etc/lightdm/lightdm.conf
找到 [Seat:*] 下的 #autologin-user= ，将这个配置修改为你需要登录的用户

[Seat:*]
...
autologin-user=radxa
autologin-user-timeout=0
...
```

## 语言设置

1. 安装简体中文字体：

```
sudo apt-get install fonts-wqy-zenhei
```

2. 设置系统语言为中文桌面：

```
sudo dpkg-reconfigure locales
```

3. 选择中文语言

![set language1 ](/img/zero/zero3w/set-language1.webp)

![set language2 ](/img/zero/zero3w/set-language2.webp)

4. 重启系统后即可

```
sudo reboot
```

其他语言的配置可以参照上述配置步骤。

## 远程登录

### SSH 登录

在连接上网络后可以通过 SSH 远程调试，官方Debian 镜像已默认开启 SSH ,只需要获取到板子的 IP 即可使用 SSH 连接。

- Debian/Ubuntu

```
ssh [username]@[hostname]
or
ssh [username]@[IP address]
例如：
ssh radxa@192.168.1.100
输入用户密码后即可连接到Debian系统。
```

- Windows

Windows 有许多 SSH 工具，这里以 [Mobaxterm](https://mobaxterm.mobatek.net/) 为你展示连接方法

点击左上角的 `Session` 新建 SSH 连接，在 `Remote host` 处输入板子的 IP，勾选 `Specify usernema` 并填入登录的用户, 双击会话开始连接后输入登录密码即可连接。

![mobaxterm ssh ](/img/zero/zero3w/mobaxterm-ssh.webp)

### VNC 远程桌面

- 安装 VNC 服务器

1. 安装 TigerVNC Server 和 dbus-x11 依赖项

```
sudo apt-get update
sudo apt-get install tigervnc-standalone-server
sudo apt-get install dbus-x11
```

2. 安装后完成VNC服务器的初始配置，请使用vncserver命令来设置安全密码并创建初始配置文件：

```
vncserver
```

:::tip
Would you like to enter a view-only password (y/n)? n 提示是否只是观看，建议选择no，输入n，这样远程就可以操作，而不是仅仅观看，可以自身实际情况选择
:::

3. 配置 VNC 服务器

```
vncserver -kill :*
touch ~/.vnc/xstartup
chmod +x ~/.vnc/xstartup
```

编辑 `~/.vnc/xstartup`，将下列的配置复制进去并保存

```
#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
unset XDG_RUNTIME_DIR
/etc/X11/xinit/xinitrc
[ -x /etc/vnc/xstartup  ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
#vncconfig -iconic &
startkde &
```

4. 配置编辑好后，重新启动VNC服务器：

```
vncserver -localhost no
```

5. 查看 VNC 服务器

```
radxa@radxa-zero3:~$ vncserver -list

TigerVNC server sessions:

X DISPLAY #     RFB PORT #      PROCESS ID      SERVER
:1              5901            4029 (stale)    Xtigervnc
```

6. 使用 mobaxterm 连接远程桌面

点击左上角的 `Session` 新建 VNC 连接，在 `Remote hostname of IP address` 处输入板子的 IP，Port为 `vncserver -list` 获取到的端口号

![mobaxterm vnc ](/img/zero/zero3w/mobaxterm-vnc.webp)

## 音视频

## 聊天视频

## 游戏

## 办公

## Android In Container
