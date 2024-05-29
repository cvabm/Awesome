### 远程命令
- `telnet x.x.x.x 22022` -> root 、password
- `ssh root@x.x.x.x 22022` -> password

### 远程工具
- xshell + xftp
  - xshell -> 工具栏 ->点击新建文件传输按钮 -> xftp  
- winscp + putty

    
- winscp
  - 协议FTP -  配置ip - 端口一般为21 ；输入账号密码
  - 使用WINSCP编辑文件时报错：加载文件时发生错误，使用936（ANSI/OEM-简体中文GBK）编码  - 需配置编辑器
  - 复制文件：直接左右拖拽

### 抓包
- `ifconfig` 获取网卡名 ，比如如eno2
-  `tcpdump -i eno2 -w temp.pcap`


## 工具下载地址
xshell+xftp 破解版
版本6：https://www.banwagongzw.com/194.html   
版本5：https://www.banwagongzw.com/108.html   
winscp：官网
