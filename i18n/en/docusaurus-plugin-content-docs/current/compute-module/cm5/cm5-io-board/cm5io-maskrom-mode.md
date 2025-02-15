---
sidebar_position: 8
---

# Masroom Mode

The Radxa CM5 supports Maskrom mode, a special mode of operation in which the CPU receives commands through the USB OTG port.
This guide will instruct you how to put the Radxa CM5 into Maskrom mode for operation.

## Preparation

- Radxa CM5 SBC
- 12V DC power adapter
- USB-A to USB-A adapter cable

## Steps

1. Install the development tool

   <Tabs queryString="host_os">
   <TabItem value="Windows">

   Use RKDevTool for Windows, please refer to [RKDevTool Guide](/general-tutorial/rksdk/rkdevtool) for installation and tutorial.

   </TabItem>
   <TabItem value="Linux_MacOS">

   For Linux and MacOS, you can use rkdeveloptool and upgrade_tool.  
   Please refer to [rkdeveloptool guide](/general-tutorial/rksdk/rkdeveloptool) and [upgrade_tool guide](/general-tutorial/rksdk/upgrade_tool) for installation and tutorial.

   </TabItem>
   </Tabs>

2. Remove microSD card etc.

3. Connect the USB-A end of the USB-A to USB-C adapter cable to the host port and the USB-C end to the OTG port (type-c port next to the headphone port) of the Radxa CM5, as shown below

   ![OTG connection](/img/cm5/cm5io-otg-connect.webp)

4. Long press Maskrom key on CM5

   ![Long press maskrom key](/img/cm5/cm5-maskrom-key.webp)

5. Power on the device and check if it has successfully entered Maskrom mode by using the corresponding tool, the following is an example of the correct entry.

   <Tabs queryString="app">
   <TabItem value="RKDevTool">

   ![Connect SPI Pin](/img/configuration/rkdevtool-maskrom.webp)

   </TabItem>
   <TabItem value="rkdeveloptool">

   ```bash
       sudo rkdeveloptool ld # List connected devices
       DevNo=1 Vid=0x2207,Pid=0x350b,LocationID=106 Maskrom
   ```

   </TabItem>
   <TabItem value="upgrade_tool">

   ```bash
       $ sudo . /upgrade_tool # List connected devices
       Using /home/rock/Linux_Upgrade_Tool/config.ini
       Program Log will save in the /root/upgrade_tool/log/
       List of rockusb connected
       DevNo=1 Vid=0x2207,Pid=0x350b,LocationID=21 Mode=Maskrom
       Found 1 rockusb,Select input DevNo,Rescan press <R>,Quit press <Q>:
   ```

   </TabItem>
   </Tabs>
