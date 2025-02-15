---
sidebar_position: 10
---

# 音频介绍

系统默认声音输出优先级为：蓝牙音频>耳机>HDMI音频。 手动选择音频输出后，该选择将被提升到最高优先级。

这意味着连接其他音频设备不会在设备以最高优先级设备播放时切换音频输出。

## 音频设置

除了图形界面，我们还可以从终端设置音频。

### 桌面设置

左键单击桌面任务栏上的音量图标会调出音频输出选择器，你可以在内部音频输出之间进行选择，同时你也可以选择任何外部音频设备，例如 USB 声卡和蓝牙音频设备。

![audio manager](/img/configuration/audio_manager.webp)

### 命令行配置

我们提供了`alsamixer`用于音量管理，通过这个命令进入设置UI：

```
radxa@rock-5a:~$ alsamixer
```

使用`up`和`down`箭头键调节音量。

```
┌────────────────────────────── AlsaMixer v1.2.4 ──────────────────────────────┐
│ Card: PulseAudio                                     F1:  Help               │
│ Chip: PulseAudio                                     F2:  System information │
│ View: F3:[Playback] F4: Capture  F5: All             F6:  Select sound card  │
│ Item: Master                                         Esc: Exit               │
│                                                                              │
│                                     ┌──┐                                     │
│                                     │  │                                     │
│                                     │  │                                     │
│                                     │  │                                     │
│                                     │  │                                     │
│                                     │  │                                     │
│                                     │  │                                     │
│                                     │▒▒│                                     │
│                                     │▒▒│                                     │
│                                     │▒▒│                                     │
│                                     │▒▒│                                     │
│                                     │▒▒│                                     │
│                                     ├──┤                                     │
│                                     │OO│                                     │
│                                     └──┘                                     │
│                                    50<>50                                    │
│                                  < Master >
```

切换其他音频输出设备，首先要知道连接了哪些设备，下面提供了一个搜索方法：

```
radxa@rock-5a:~$ pacmd list-sinks | grep -e 'index:' -e 'name:'
```

您将看到连接的音频设备的索引和名称，如下所示：

```
    index: 0
        name: <alsa_output.platform-dp0-sound.HDMI__hw_rockchiphdmi1__sink>
    index: 1
        name: <alsa_output.platform-es8316-sound.HiFi__hw_rockchipes8316__sink>
  * index: 7
        name: <bluez_sink.C0_09_0B_48_26_53.a2dp_sink>
```

带有“\*”的索引表示它是最高优先级的设备。  
以下命令将帮助您更改默认输出设备：

```
radxa@rock-5a:~$ pacmd set-default-sink alsa_output.platform-es8316-sound.HiFi__hw_rockchipes8316__sink  # 'alsa_output.platform-es8316-sound.HiFi__hw_rockchipes8316__sink' is the name of the device you want to set.
```

想了解更多信息，请查看 [pacmd page](https://man.archlinux.org/man/extra/pulseaudio/pacmd.1.en).
