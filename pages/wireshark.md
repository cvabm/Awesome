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
## 工具下载地址
xshell+xftp 破解版
版本6：https://www.banwagongzw.com/194.html   
版本5：https://www.banwagongzw.com/108.html   
winscp：官网
### 抓包
- `ifconfig` 获取网卡名 ，比如如eno2;  `tcpdump -i eno2 -w temp.pcap`
### 分析h264码流

> 6.右键点击H264的udp包，选择"Decode as..."，再选择Transport中的rtp选项，就解析成rtp包了
> 
> 7.查看rtp包的payload type，比如说type是96，那么在wireshark工具栏选择Edit->preferences->protocols->H264, 把H264 dynamic payload types设成96
>
> 8.现在就可以选择点击tools下的"Extract h264 stream from RTP"菜单项
>
> 9.这样就可以生成dump.264，一般会放在与码流文件同一个路径下，由于环境变量的不同，也可能放在其他路径下
>
> 10.该文件rtp_h264_extractor.lua目前已经支持了排序，FU-A，STAP-A等常见的rtp h264打包方式
>
>抓取一个包含H.264 Payload RTP包的SIP会话或RTSP会话后，用Wireshark的Play功能只能播放声音，不能播放视频。把RTP payload直接导出成文件后也是不能直接播放的，因为H.264 over RTP封包是符合RFC3984规范的，必须按照该规范把H.264数据取出来后，组成NALU，放到avi/mp4或裸码流文件等容器里后才能播放。
>
### 常用过滤
> `ip.src == 10.166.18.207 && udp.port == 10000` 过滤制定ip + udp端口
> h264

### 乱序丢包
