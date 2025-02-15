---
sidebar_position: 10
---

# 无屏模式简介

本指南旨在指导您在没有键盘或显示器的情况下使用，也被称为无屏模式。

在第一次启动时，SSH服务会在没有连接显示器的情况下自动启用。尽管这样，你还需要将其连接到局域网，这样你才可以得到SBC的**_IP地址_**。

## 以太网

网络设置可以参考这个指南： [网络指南](/radxa-os/config/network.md)。
通过有线连接将SBC连接到与你的计算机**相同的网络**。

## 无线网

The [wireless guide](/radxa-os/config/network.md) may be helpful.

_注意：有些产品需要安装WiFi模块来连接到无线网络。更多细节，请在[产品介绍](https://radxa.com/products)上查看产品参数。_

将系统镜像烧写到 microSD 卡后不要从你的Linux或Windows机器拔出， 可以在文件系统中找到配置文件夹。其中有两个文件**before.txt\*和**config.txt\*\*。

**before.txt**： Radxa首次启动配置，它将被复制到Linux根文件系统的正确位置，机器将使用这些设置来启动无线网络。

**config.txt**：rsetup配置文件，它将在每次启动时应用。

要启用自动Wi-Fi连接，在**before.txt**中添加以下一行：

```
connect_wi-fi YOUR_WIFI_SSID YOUR_WIFI_PASSWORD
```

## 获取IP地址

相对来说， 使用串口工具连接SBC和你的电脑后会更简单：  
请参考[串口通信指南](https://wiki.radxa.com/Rock5/dev/serial-console)。

- 通过串口通讯软件如`putty`或`minicom`访问终端。
- 将机器开机并等待登录提示。
- 用默认账户登录。
- 运行`ip a`来查询IP地址。

你也可以从你的路由器IP管理界面来查询IP。请参考你的路由器制造商的文档。

## SSH连接

请查阅[SSH指南](remote-login)。

安装ssh服务后，通过用户名和ip地址直接在终端上进行远程连接，如以下代码：
`ssh <username>@[IP address]`

例如： `ssh radxa@192.168.42.100`.
![ssh connect](/img/configuration/ssh-connect.webp)
