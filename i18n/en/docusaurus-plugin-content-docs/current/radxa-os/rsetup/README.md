---
sidebar_position: 0
---

# `rsetup`

`rsetup` is a system configurator developed by Risa.

To start `rsetup`, execute the `rsetup` command directly in a terminal, or find the `rsetup` application from the system menu:

:::caution
`rsetup` requires administrator privileges to run. Please make sure you have `sudo` privilege.
:::

```
┌──────────────────────────────────┤ RSETUP ├──────────────────────────────────┐
│ Please select an option below:                                               │
│                                                                              │
│                             System Maintenance                               │
│                             Hardware                                         │
│                             Overlays                                         │
│                             Connectivity                                     │
│                             User Settings                                    │
│                             Localization                                     │
│                             About                                            │
│                                                                              │
│                     <Ok>                         <Cancel>                    │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

:::caution
The options listed above are for reference only. Please refer to the actual program output.
:::

## Interface Operation

Use the `Up` and `Down` keys to select between the menu options. The currently selected item is highlighted.

Use the `Tab` key to select between the menu area and the command area.

Use the `Left` and `Right` keys to toggle between the `<Ok>` and `<Cancel>` commands. Use the `Enter` key to execute the selected command.  
Pressing the `Enter` key, when the command area is not selected, will immediately execute the `<Ok>` command.

Use the `Space` key to select items. Items are prefixed with `[ ]` (indicating multiple selections) or `( )` (indicating single selection) to show the current selection status.

:::caution
Using the `Enter` key does not select any item. It executes the `<Ok>` command directly.
:::.

Use the `Esc` key to return to the previous menu.

## System Maintenance

This menu contains the following options:

```bash
┌──────────────────────────────────┤ RSETUP ├──────────────────────────────────┐
│ System Maintenance                                                           │
│                                                                              │
│                         System Update                                        │
│                         Update Bootloader                                    │
│                         Update SPI Bootloader                                │
│                         Update eMMC Boot partition                           │
│                                                                              │
│                     <Ok>                         <Cancel>                    │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### System Update

This option will update the packages installed on your system to the latest release.

Since RadxaOS provides some packages that conflict with the upstream Debian, it is recommended to update your system in this way to ensure system consistency.

### Update Bootloader

:::caution
Updating the bootloader carries the risk that the system may not boot. Please perform this operation only if the data has been backed up.
:::

This option updates the bootloader on the disk where the root file system is located.

:::warning
This option only applies to scenarios where the boot device and the system device are the same.  
This option can be used if you are booting directly after installing the system (i.e., without setting up customized boot options).
:::

### Update SPI Bootloader

:::caution
Updating the bootloader carries the risk that the system may not boot. Please perform this operation only if the data has been backed up.
:::.

This option updates the bootloader on the SPI Flash.

:::tip
This option is for scenarios where you need to boot from an NVMe SSD or USB mass storage device.  
Not all products support SPI booting.
:::.

### Update eMMC Boot partition

:::caution
Updating the bootloader carries the risk that the system may not boot. Please perform this operation only if the data has been backed up.
:::.

This option updates the bootloader on the eMMC Boot partition.

:::tip
This option is for scenarios where you need to boot from an NVMe SSD or USB mass storage device.  
Not all products support booting from an eMMC Boot partition.  
Rockchip SoC-based products do not support eMMC Boot partition booting.
:::

## Hardware

Some peripherals can be modified on this menu, the following is the introduction of them.

```
┌──────────────────────────────────┤ RSETUP ├──────────────────────────────────┐
│ Manage on-board hardware                                                     │
│                                                                              │
│                      Video capture devices                                   │
│                      GPIO LEDs                                               │
│                      Thermal governor                                        │
│                      Configure DSI display mirroring                         │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                     <Ok>                         <Cancel>                    │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

### Video capture devices

If you have connect a video device, this option can help you to capture an image for testing.

### GPIO LEDs

On this option, you can change the status of power LED and user LED on the board (Sometimes only one).  
For the details, please refer to the [LED Setup](/radxa-os/rsetup/led).

### Thermal governor

This module is used to adjust the fan and other temperature options.  
Generally, we select `power_allocator` when using DC fan or fanless, select `step_wise` when using PWM fan.  
**Note: If you connect the fan directly to the GPIO on 5V and GND pins, it would not be controlled and always work.**

### Configure DSI display mirroring

If DSI display has some problems when using HDMI display and DSI display at the same time, enable this option will helpful.

## Overlays

This option is for Configure Device Tree Overlay, please check [Device Tree Configuration](/radxa-os/rsetup/devicetree) for more information.

## Connectivity

This option is normally similar to [Network Setting](/radxa-os/config/network.md).

## User Settings

The `Password` of the current login account and the `Hostname` of the device can be changed on this option.

## Localization

On this option, you can change `Timezone` `Locale` `Keybaed layout` `Wi-Fi Country`.

## About

Here is the information of `rsetup`.
