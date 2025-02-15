---
sidebar_position: 40
---

# 更换语言

## 更改系统语言

**注意：**系统默认设置为英文，如需其他语言，请按照以下说明操作。

在系统设置中，点击区域设置添加语言。

![rock5a_system_language_1](/img/rock5a/rock5a_system_language_1.webp)

选择您想要的语言并单击添加。

![rock5a_system_language_2](/img/rock5a/rock5a_system_language_2.webp)

在新语言列中，单击向上图标提升为默认语言，然后单击应用。 重新启动计算机，系统语言将设置为新语言。

![rock5a_system_language_3](/img/rock5a/rock5a_system_language_3.webp)

## 更改语言输入法

Debian系统默认只有英文输入法，如果需要其他语言的输入法，需要单独安装。 这里我们举例说明如何安装拼音。

### 环境配置

如果使用的Debian环境不是中文环境，需要切换到中文环境，可以使用如下命令切换，然后输入用户密码

    sudo dpkg-reconfigure locales

按空格或回车选择确定，准备下一步安装。

![rock5a_language_input_1](/img/rock5a/rock5a_language_input_1.webp)  
![rock5a_language_input_2](/img/rock5a/rock5a_language_input_2.webp)

执行以下命令更新并安装系统环境软件：

    sudo apt update

### 安装fcitx中文输入法

1.  打开命令终端并输入以下命令：

    sudo apt install fcitx  
    输入“Y”，将安装包。

2.  执行你需要安装的中文输入法命令，然后输入用户密码。

        sudo apt install fcitx-googlepinyin

    输入“Y”完成安装。

安装成功后，请重启电脑，电脑任务栏会显示键盘图标。

右键单击键盘图片，然后单击配置

![rock5a_language_input_3](/img/rock5a/rock5a_language_input_3.webp)

点击“+”添加新的语言输入法。

![rock5a_language_input_4](/img/rock5a/rock5a_language_input_4.webp)

点击方框取消 "only show current language"

![rock5a_language_input_5](/img/rock5a/rock5a_language_input_5.webp)

在搜索框中输入*Google pinyin*，点击确定，完成添加新的语言输入法。

![rock5a_language_input_6](/img/rock5a/rock5a_language_input_6.webp)

单击 ^ 调整语言优先级，如图所示。

![rock5a_language_input_7](/img/rock5a/rock5a_language_input_7.webp)

现在您可以开始使用拼音了。如果要切换语言，只需点击键盘图标即可切换语言输入法。

![rock5a_language_input_8](/img/rock5a/rock5a_language_input_8.webp)

# 键盘布局

在系统界面打开`Input Devices`。

![rock5a_keyboard_1](/img/rock5a/rock5a_keyboard_1.webp)

单击`Layouts`，然后单击`Add`以选择所需的键盘布局。

![rock5a_keyboard_2](/img/rock5a/rock5a_keyboard_2.webp)

选择`Limit selection by language` 或 `layout` 来设置你想要的键盘布局，你可以点击`Preview`查看。

![rock5a_keyboard_3](/img/rock5a/rock5a_keyboard_3.webp)

你可以点击`Move up`提升优先级然后点击`Apply`.

![rock5a_keyboard_4](/img/rock5a/rock5a_keyboard_4.webp)
