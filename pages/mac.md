# mac

slug: mac
status: Published
tags: other
type: Post

### mac基本设置

## 常用命令

> zsh切换为bash
> 

`chsh -s /bin/bash`

bash切换为zsh

`chsh -s /bin/zsh`

当然，输入完密码之后，需要重启或者新开窗口。

> 反向Tab
> 

`shift + tab`

> 返回顶部
> 

`command + ↑`

> 撤销操作
> 

`command + z`

> 恢复操作
> 

`command + shift + z`

## 常用软件使用

推荐应用

[https://wangchujiang.com/awesome-mac/index.zh.html](https://wangchujiang.com/awesome-mac/index.zh.html)

下载站

[https://xclient.info](https://xclient.info/)

[https://www.macdo.cn](https://www.macdo.cn/)

[https://www.macapp.so](https://www.macapp.so/)

### alfred

快捷键

调用 ：option + 空格

剪切板 ：option + command +c

搜索书签： bm +关键字

### 虚拟机

[https://xclient.info/s/vmware-fusion.html](https://xclient.info/s/vmware-fusion.html)

相关问题：

不能为虚拟电脑打开一个新的任务

```

惠普进入bios ----  开机按 F10 --  security ----- virtual su------ 设置为abled
选中你的虚拟机， 设置--- 存储 ---选择控制器-ide下边的光盘----选择分配光驱后的光盘---
选择iso文件 ---安装----

在邮编单击storage,在存贮树中选中光驱，
在属性中单击右边的小光盘标志，单击“choose a virtru..."，
浏览到你的影像就可以了
```

共享粘贴板

```
设置－－存储　－－－控制器　－－－－选中使用Ｉ０输入输出。。。。
我的计算机－－－cd驱动器　－－－安装ｖｂｏｘｗｉｎｄｏｗ。。。
设置－－－共享文件夹　－－－
正在设定 ttf-mscorefonts-installer
```

```
ubuntu,在安装wine时停在了“正在设定 ttf-mscorefonts-installer”,怎么确定啊：
TAB 选择确定吧
安装gradle
```

[https://www.jianshu.com/p/c28062f94809](https://www.jianshu.com/p/c28062f94809)

### 屏幕取色

应用 - 数码调色器 - 设置显示为十六进制

复制 shift + command + c

粘贴 shift + command + v

## mac快捷键

常用

```

Command-Z   撤消上一命令（有些 app 可让您撤消多次）
Command-Shift-4 将所选屏幕内容捕捉到一个文件，或按空格键仅捕捉一个窗口
Command-H   隐藏当前正在运行的 app 的窗口
fn-Delete   向前删除（适用于便携式 Mac 的内建键盘）
fn-上箭头  向上滚动一页（相当于 Page Up 键）
fn-下箭头  向下滚动一页（相当于 Page Down 键）
fn-左箭头  滚动至文稿开头（相当于 Home 键）
fn-右箭头  滚动至文稿末尾（相当于 End 键）
control + command + q 锁屏
Command-减号 (–)  缩小所选项
Command-加号 (+)或 Command-Shift-等号 (=)    放大所选项
```

```

组合键 功能
Command-C   将所选数据拷贝到剪贴板
Command-X   移除选中的项目，然后将副本放在剪贴板中
Command-V   将剪贴板副本放到（粘贴）到当前文稿或 app 中
Command-Shift-3 将屏幕捕捉到文件
Command-Shift-Control-3 将屏幕内容捕捉到剪贴板
Command-Shift-4 将所选屏幕内容捕捉到一个文件，或按空格键仅捕捉一个窗口
Command-Shift-Control-4 将所选屏幕内容捕捉到剪贴板，或按空格键仅捕捉一个窗口
电源按钮    轻按可开机。在通电后，轻按“电源”按钮可使您的 Mac 唤醒或进入睡眠状态。
按住电源按钮 1.5 秒    显示重新启动/睡眠/关闭对话框
按住电源按钮 5 秒  强制 Mac 关机

Control-电源按钮    显示重新启动/睡眠/关闭对话框

Command-Control-电源按钮    强制 Mac 重新启动

Command-Option-电源按钮 使电脑进入睡眠状态

Command-Control-电源按钮    退出所有 app（会让您先存储对已打开文稿所作的更改），然后重新启动电脑

Command-Option-Control-电源按钮 退出所有 app（会让您先存储对已打开文稿所作的更改），然后关闭电脑

Shift-Control-电源按钮  使所有显示器进入睡眠状态

Command-Shift-Q 注销

Command-Shift-Option-Q  立即注销

```

## 常见问题

### Mac上“查询”后总显示“找不到结果” 、无法添加欧路词典

```

最佳解决方案是删除

/System/Library/AssetsV2/PreinstalledAssetsV2/InstallWithOs/com_apple_MobileAsset_DictionaryServices_dictionaryOSX

路径下的所有文件夹

删除之后在词典里点击相应词典就可以重新下载添加了

```

### chrome访问https证书问题

Chrome NET::ERR_CERT_INVALID解决办法

```

 There's a secret passphrase built into the error page.  Just make sure the page is selected (click anywhere on the background), and type `thisisunsafe`

```

## 设置截图默认保存位置

```

创建一个用来保存平时截图的目录，如：mkdir ~/Desktop/idolaoxuPic

在mac终端执行命令：

defaults write com.apple.screencapture location ~/Desktop/idolaoxuPic

如下执行完后，修改并没有生效，需执行如下命令生效

killall SystemUIServer

```

## 打开摄像头

photo booth

### mac输入法卡顿

通用 - 安全与隐私- 文件保险箱 - 关闭

### safari切换tab

command + shift + left/right

### 强制退出软件

同时按住三个按键：Option、Command 和Esc (Escape) 键。 或者，从屏幕左上角的苹果菜单 中选取“强制退出”。 （这类似于在PC 上按下Control-Alt-Delete。） 然后，在“强制退出”窗口中选择相应的App 并点按“强制退出”。

### chrome快捷键(mac)

> 下一个Tab: Control + Tab
> 

前一个Tab: Control + Shift + Tab

### mac配置adb

```

vi ~/.bash_profile
加入：
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/emulator
第一行为sdk所在目录，然后source启用即可

source ./bash_profile

```

### mac更新adb