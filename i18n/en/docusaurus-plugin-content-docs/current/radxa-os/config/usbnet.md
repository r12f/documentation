---
sidebar_position: 10
---

# USB Networking

Most of radxa products have reserved a USB port as an OTG port, it also a adb debug port when runuing Android. You can consult the port definitions of the corresponding [products](https://radxa.com/products).  
You can set up a shared network between two products by connecting their OTG ports. Now officially supported for latest linux and android images.

## Preparations

**Cable**: Before you start, you will need one USB-A to USB-A cable to connect two SBCs.

**Software**: If your SBC has not the latest software, connect you SBC to internet and type the following command:

```
sudo apt update && sudo apt full-upgrade
```

**Service**: After updating software, you need to start the `radxa-usbnet` service:

```
sudo systemctl enable --now radxa-usbnet
```

**Status**: Typing the command to confirm if the service is running:

```
sudo systemctl status radxa-usbnet.service
```

The service active status is usually `active(exited)` when running.

## OTG Settings

At first, connect the two SBC OTG ports by USB-A to USB-A cable.  
Device identity of this shared network depends on what [overlay](/radxa-os/rsetup/devicetree) you enable,the host machine shares the network to device mahine.  
The host machine enable this overlay:

```
		[*] Set OTG port to Host mode
```

The device machine enable this overlay:

```
		[*] Set OTG port to Peripheral mode
```

Reboot after enable options.

### To the Host machine

For sharing the network to device machine, host machine need to connect to the external network, both wired and wireless networks are available.  
Next, we need to set up a shared adapter for the device machine connection, which can be set on the KDE Desktop and Terminal.  
This guide you set it on terminal:

**Set shared adapter:**

Before operating, confirm if there is a new networkcard device:

```
radxa@rock-5a:~$ ip a
```

The name of it may be different:

```
3: enxca5bfb533dd4: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether ca:5b:fb:53:3d:d4 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::b989:8daf:feb5:f020/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

If there is not a new network card, you may need to set overlay once again.

Network Manager Tool is the recommended tool to manage the network, typing the command to open the interface:

```
radxa@rock-5a:~$ sudo nmtui
```

After identification, the setting interface appears:

```
                              NetworkManager TUI

                            Please select an option

                            Edit a connection
                            Activate a connection
                            Set system hostname

                            Quit

                                              <OK>
```

Select `Edit a connection -- <Add>` to add a `Ethernet` adapter:
![add adapter](/img/configuration/add_adapter.webp)  
Of the many options, we only need to fill in two of them:

```
        Device____  # Enter the third network card name you get by 'ip a', like: enxca5bfb533dd4
        IPv4 CONFIGURATION <Shared> # Change <Automatic> to <Shared>
```

Save the configuration and return to setting interface to `Activate a connection`, select the option you just add.  
It would be following if you apply it right:

```
                USB Ethernet
                    * Ethernet connection 1
```

**Confirm adapter setting:**  
After you settings, check if there is a IP address of third network card:

```
radxa@rock-5a:~$ ip a
```

The expected output result is like following:

```
3: enxca5bfb533dd4: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether ca:5b:fb:53:3d:d4 brd ff:ff:ff:ff:ff:ff
    inet 10.42.0.1/24 brd 10.42.0.255 scope global noprefixroute enxca5bfb533dd4
       valid_lft forever preferred_lft forever
    inet6 fe80::e37c:5ced:58a8:ec32/64 scope link noprefixroute
       valid_lft forever preferred_lft forever

```

If it's similar with your result, time to set up device machine.

### To Device machine

**Enable usb network connection:**
Relative to Host machine, it woulb be easy for device machine settings.  
At first, enable the `Set OTG port to Peripheral mode` overlay and start the `radxa-usbnet` service, reboot.  
Typing `ip a` to confirm if a new device named `usb0` like the following added:

```
3: usb0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo_fast state DOWN group default qlen 1000
    link/ether 76:c7:9d:9e:d5:da brd ff:ff:ff:ff:ff:ff
```

If not, check previous steps: reopen the overlay (Don't forget to reboot.) and restart the usbnet service.

**Set up usbnet adapter:**
Next, set up the adapter as set up the Host device:  
Open the Network Manager Tool:

```
radxa@rock-5a:~$ sudo nmtui
```

Select `Edit a connection -- <Add>` to add a `Ethernet` adapter:

Only the Device option should be modify, type 'usb0':

```
Device usb0
```

Other options remain default. Save the configuration.

**Connect to Host device:**

Return to setting interface to `Activate a connection`, select the option you just add.

```
                Ethernet (usb0)
                    Ethernet connection 1
```

It would take a few seconds to connect to Host device.

**Check the connection:**

Check if usb0 get the IP address like following:

```
radxa@rock-5a:~$ ip a

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000
    link/ether f2:44:7d:ac:20:85 brd ff:ff:ff:ff:ff:ff
3: usb0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 76:c7:9d:9e:d5:da brd ff:ff:ff:ff:ff:ff
    inet 10.42.0.46/24 brd 10.42.0.255 scope global dynamic noprefixroute usb0
       valid_lft 3597sec preferred_lft 3597sec
    inet6 fe80::1031:1ee2:bcee:4855/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

If the Host machine connect to ethernet, Device machine can also connect now.
