---
sidebar_position: 10
---

# Configure the UART2_M0 interface as a normal serial port

:::info
By default, the UART2_M0 interface is a FIQ debugging serial port, which can output logs of DDR Init, U-Boot, Linux Kernel and other logs for debugging. Therefore, it is not recommended to cancel this configuration as you can use other serial ports if not necessary.
:::

## Preparation

- A Radxa single board computer or computing module running an official Radxa distribution system

## Start rsetup and enter the Manage overlays interface

```bash
rsetup
```

## After entering rsetup, follow [Device Tree Configuration](/radxa-os/rsetup/devicetree) to enter the Manage overlays interface

## Configure UART2_M0 as a normal serial port.

### Check `Enable UART2-M0`

![Enable UART2-M0](/img/general-tutorial/EnableUART2-M0.webp)

### Select OK, then exit rsetup.

## Modify Linux boot parameters

Following [Modify Linux boot parameters](/radxa-os/config/cmdline), remove all console parameters related to ttyFIQ0 and ttyS2 when doing `sudo nano /etc/kernel/cmdline` operations, such as "console=ttyFIQ0, 1500000n8"
