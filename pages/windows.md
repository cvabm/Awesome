# windows

slug: windows_app
status: Published
tags: 开发工具
type: Post

### 常用命令

- `start .`或者`explorer .`打开当前路径的文件夹
- `df -h` disk free
- `tasklist | findstr "nginx"` 查看某服务是否运行
- `taskkill /F /IM nginx.exe` 停止服务
- `taskkill /F /PID 118028`

### windows/问题

- **“ipconfig 不是内部命令或外部命令”解决方法**

配置环境变量

Path 加入内容“c:\windows\system32”

### ****WIN10蓝屏终止代码：inaccessible boot device解决办法****

[https://zhuanlan.zhihu.com/p/519845612?utm_id=0](https://zhuanlan.zhihu.com/p/519845612?utm_id=0)

### 蓝牙鼠标休眠导致卡死问题

- 右键点击开始菜单，打开设备管理器，找到蓝牙，右键点击 英特尔 无线 Bluetooth ，打开属性。
- 在 电源管理 选项卡上, 取消选中 “允许计算机关闭此设备以节省电源” 选项，保存即生效。不是所有蓝牙模块都有电源管理选项，没有这个选项的一般也不会自动关闭。


### 打包exe程序
- exe4j jar打包成exe
- 
