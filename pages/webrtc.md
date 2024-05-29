# webrtc

slug: webrtc  
status: Published  
tags: react  
type: Post

## 源码

[https://github.com/DrKLO/Telegram/blob/master/TMessagesProj/jni/voip/webrtc/media/engine/webrtc_video_engine.cc#L1254](https://github.com/DrKLO/Telegram/blob/master/TMessagesProj/jni/voip/webrtc/media/engine/webrtc_video_engine.cc#L1254)

[https://webrtc.googlesource.com/src/+/50cfe1fda7f2b4a6a449fe7234f4c1aa2a475c61/webrtc/media/engine/webrtcvideoengine2.cc](https://webrtc.googlesource.com/src/+/50cfe1fda7f2b4a6a449fe7234f4c1aa2a475c61/webrtc/media/engine/webrtcvideoengine2.cc)

## 开启日志

`Logging.enableLogToDebugOutput(Logging.Severity.LS_VERBOSE)` ## webrtc-android源码编译 [https://juejin.cn/post/6956379281907777572](https://juejin.cn/post/6956379281907777572)

[https://blog.jianchihu.net/webrtc-android-build-guide.html](https://blog.jianchihu.net/webrtc-android-build-guide.html)

**depot_tools/ninja.py: Could not find Ninja in the third_party of the current project, nor in your PATH.**

新版本问题，需手动安装ninja

`sudo apt install ninja-build` ## WebRTC 端到端连接建立过程！！

**1. A 获取媒体流(MediaStream)或数据流。**

```java

一般通过MediaDevices.getUserMedia()获取媒体流，媒体流包含了请求媒体类型的（音视频）轨道(MediaStreamTrack)。
一个流可以包含视频轨道，音频轨道或其他。通过MediaStream的addTrack方法可以添加轨道。
 关于MediaDevices参考https://developer.mozilla.org/zh-CN/docs/Web/API/MediaStream。

```

**2. A 生成一个 RTCPeerConnection 接口对象**

````
RTCPeerConnection接口代表一个由本地计算机到远端的WebRTC连接。该接口提供了创建，保持，监控，关闭连接的方法的实现。

pc = new RTCPeerConnection([RTCConfiguration dictionary]) //可选参数包括ice服务器等。

````

**3. A 将流加入到 RTCPeerConnection 对象中**

````
pc.addStream(stream);//该方法已经不推荐使用，推荐使用addTrack

//或者加入轨道stream.getTracks().forEach(track => pc.addTrack(track, stream));

````

**4. A 生成 Offer 信息**

````
pc.createOffer(function(offer)=>{//创建完成 TODO 5},error)

````

**5. A 将生成的 Offer 设置为本地描述。**

````
pc.setLocalDescription(new RTCSessionDescription(offer),function(){

//设置完成 TODO 6},error);

````

**6. A 将生成的 Offer 发给另一端 B（服务器中转）**

````
send json.stringify(offer)

````

**7. B 也生成 RTCPeerConnection，并按需求设置流。**

````
new RTCPeerConnection()

````

**8. B 将收到的 Offer 设置为远端描述。**

````
pc.setRemoteDescription(new RTCSessionDescription(Json.parse(offerString)),function(){//设置完成 TODO 9},error);

````

**9. B 生成 Answer，并设置为本地描述。**

````
pc.createAnswer(function(answer){pc.setLocalDescription(new RTCSessionDescription(answer),function(){ //设置完成，TODO 10 })},error)

````

**10. B 把 Answer 发送给发起方 A(服务器中转)**

````
send json.stringify(answer)

````

**11. A 将 Answer 设置为远端描述。**

````
pc.setRemoteDescription(new RTCSessionDescription(Json.parse(answerString)),function(){//设置完成 TODO 9},error);

````

**12. 交换 ICE 候选地址信息**

````
建立连接过程中，会回调onicecandidate事件，传递ICE候选地址，我们需要将其转发至另一端，并通过另一端的方法addIceCandidate方法设置对方的候选地址。
pc.onicecandidate = function(event) {if (event.candidate)
 { // 发送 let iceinfo = event.candidate 至另一端 }
  else
   { // All ICE candidates have been sent }}
   //另一端//接收到上面的iceinfopc.addIceCandidate(new RTCIceCandidate(iceinfo));理想情况下，现在已经建立连接了。

交换与使用媒体流

当一方addStream或addTrack后，另一方的RTCPeerConnection会触发onaddstream或addTrack事件回调，通过事件参数可以获取对面的流或轨道数据，
以此进行媒体显示等。当前版本的协议已经不再推荐addStream方法，应使用addTrack方法。

关于硬件流

硬件只能被一个流占用，多个RTCPeerConnection可以共享这一个流。

````

## 一些 demo 和相关网站

[https://webrtc.org/getting-started/overview](https://webrtc.org/getting-started/overview)

**webrtc APIs demo 演示**

[https://webrtc.github.io/samples/](https://webrtc.github.io/samples/)

**android 原生上使用 webrtc** 包括使用相机、屏幕共享、信令交互、多人视频

[https://www.jianshu.com/p/eb5fd116e6c8](https://www.jianshu.com/p/eb5fd116e6c8)

## 基本概念

> NAT  
将内网与内网通信时怎么将内网私有 IP 地址转换为可在网络中传播的合法 IP 地址  
通过UDP 打洞实现 NAT 穿越是一种在处于使用了 NAT 的私有网络中的 Internet 主机之间建立双向 UDP 连接的方法STUN  
STUN（Simple Traversal of UDP Through NATs）其作用是进行 NAT 类型判定，对于可以穿越的 NAT 类型进行 UDP 穿越。TURN  
TURN（Traversal Using Relays around NAT），其主要作用是通过服务端进行数据转发。ICE  
ICE 跟 STUN 和 TURN 不一样，ICE 不是一种协议，而是一个 framework，它整合了 STUN 和 TURN。REMB  
REMB （Receiver Estimated Maximum Bitrate ），用于估算网络带宽。RTCP  
RTCP（The RTP Control Protocol ），RTP 控制协议。通常用于报告 RTP 数据的接收与发送数据的统计报告。RTP  
RTP（Real-time Transport Protocol ），一种网络传输协议，在 UDP 之上，通常用于音视频数据的传输。GCC  
GCC（Google Congestion Control），google 提出一套拥塞控制算法，主要有两种：一种是通过丢包率计算拥塞，另一种是通过时延计算拥塞。

***

````
RTC(Real Time Communication): 实时通信
WebRTC: 基于web的实时通信
Signaling: 信令, 一些描述媒体或网络的字符串

````

> WebRTC 逻辑相关
> 
> 在 WebRTC 中包括了 Stream, Track 和 channel 的概念。
> 
> - **Track**  
>   Track（轨）, 轨是 WebRTC 中借鉴了其它多媒体相关的概念。轨的特性大家都非常清楚，两条轨是永远不会相交的。轨用在多媒体中，表式的是每条 “轨” 数据都是独立存在的，不会与其它 “轨” 相交。如音频轨，视频轨。
> - **Stream**  
>   在 WebRTC 中分为媒流（MediaStream）和数据流（DataStream）。对于 MediaStream 是一个多条轨的集合，在它里面包括了一个终端的音频转和视频轨。
> - **Channel**  
>   Channel 是传输层面的概念，也就是音视频数据最终要交由 channel 传送出去。而 channel 最终会交由 socket 将数据发送出来。了为解耦 stream 与 socket，所以增加了 channel 的概念。
> - **sdp**  
>   SDP(Session Description Protocol) 的目的是在媒体会话中传递媒体信息。SDP 在很多地方使用，WebRTC 也会使用它做媒体信息交换。

## webrtc 视频方向的设置

````
sdp信息中包装有个a=extmap:7 urn:3gpp:video-orientation 参数

视频发送方将其视频方向进行封装（具体方式见9.3），封装以后，放在视频数据帧的一个扩展位置，然后随视频帧一起打包后通过rtp/rtcp/udp发送给接收方。
接收方收到视频帧数据后，可以在帧的扩展位置将视频方向获取出来，然后，在实时的调整到surface view上面

视频方向格式及编解码

定义在rtp帧中的扩展数据，该数据是用一个8位字节进行编码的。前面四位是预留位，用于其他将来用途，
后面四位中，从高到低，第一位是视频发送方camera的选项，可编码出2种camera选项；后三位是视频数据的方向，可以编码出8种视频方向

编码：

将camera选项位和视频方向位四位编码后的数据映射成十进制数字，就是该帧方向编码后的整数值了。
比如发送方当前是后置摄像头并且视频顺时针旋转了90度，那么四位编码则是1011，转换成十进制就是11，那么接收方通过帧中的扩展位数据得到的就是11。

位运算法则：total = (camera << 3) | orientation。

解码：

接收方的到11后，对应的转换成二进制就是1011，获取第四位就是发送方camera的选项，获取后三位就是视频的方向。

位运算法则：

Camera = (total & 0x08) >> 3;

Orientation = total & 0x07;
————————————————
版权声明：本文为CSDN博主「晓昏行者」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：<https://blog.csdn.net/liangguangxiang/java/article/details/48526219>

````

## SDP 详细介绍

**SDP 主要包括以下信息：**

````
>会话的名称与目的
>会话的存活时间
>会话中的媒体信息，这是最主要的，它又包括以下内容：
>   - 媒体类型
>   - 媒体格式
>   - 传输协议
>   - 传输的IP和端口

````

**SDP 的格式**

````
SDP是由多个<type>=<value>组成的。
其中<type>是一个字符， <value>是一个字符串。需要特别注意的是，=两边是不能有空格的。

SDP会话描述由一个会话级描述（session_level description）和多个媒体级描述（media_level description）组成。

会话级（session_level）的作用域是整个会话。其位置是从’v=’行开始到第一个媒体描述为止。

媒体级（media_level）描述是对单个的媒体流进行描述，其位置是从’m=’行开始到下一个媒体描述为止。

总之，除非媒体部分重载，会话级的值是各个媒体的缺省默认值。

````

**参数结构**

````
Version（必选）
v=0 SDP的版本号，不包括次版本号。

origion（必选）
o=<username> <session id> <version> <network type> <address type> <address>

“o=”项对会话的发起者进行了描述。
<username>是用户的登录名。如果主机不支持<username>，则为 ”－” 。
注意：<username>不能含空格。

<session id>：是一个数字串。在整个会话中，必须是唯一的。为了确保其唯一，建议使用NTP(Network Time Protocol) timestamp。
<version>：该会话公告的版本,供公告代理服务器检测同一会话的若干个公告中哪个是最新公告。基本要求是会话数据修改后该版本值递增,建议用NTP时戳。
<network type>：网络类型，一般为”IN”,表示”internet”
<address type>：地址类型，一般为IP4
<address>：地址
Session Name（必选）
s=<session name> 会话名，在整个会话中有且只有一个”s=”。

Connection Data（可选）
c=<network type> <address type> <connection address>

表示媒体连接信息。 一个会话声明中，会话级描述中必须有”c=”项或者在每个媒体级描述中有一个”c=”项。
可能在会话级描述和每个媒体级描述中都有”c=”项。

<network type>：网络类型，一般为”IN”,表示”internet”
<address type>：地址类型，一般为IP4。
<connection address>：应用程序必须处理域名和ip地址两种情形。
单播时，为域名或ip地址，推荐使用域名；
多播时，为ip地址，且ip后面必须有TTL（取值范围是0－255）。地址和TTL决定了多播包被传播的范围，例： c=IN IP4 224.2.1.1/127。分层编码方案是一个数据流被分为多层，接受者能够通过申请不同层的流选择流的质量。如下：<base multicast address>/<ttl>/<number of addresses> 如果<number of addresses>没有给定，则默认为1。 c=IN IP4 224.2.1.1/127/3 等价于： c=IN IP4 224.2.1.1/127 c=IN IP4 224.2.1.2/127 c=IN IP4 224.2.1.3/127

Bandwidth（可选）
b=<modifier>:<bandwidth-value>

描述了建议的带宽，单位kilobits per second，可选。

<modifier>：包括两种CT和AS。CT：Conference Total，总带宽。AS：Application-Specific Maximum，单个媒体带宽的最大值。 扩展机制：<modifier>以”X－”开始。建议modifier越短越好。例 b=X-YZ:128
Times（必选）
t=<start time> <stop time>

描述了会话的开始时间和结束时间。 <start time> 和<stop time> 为NTP时间，单位是秒。假如<stop time>为零表示过了<start time>时间后会话一直持续。当<start time> 和<stop time>均为零时表示持久会话。

建议start time和stop time不要设为0。因为不知道此会话的开始和结束时间，增加了调度（scheduling）的难度。

Media Announcements （必选）
m=<media> <port> <transport> <fmt list>

一个会话描述包括几个媒体描述。一个媒体描述以”m=”开始到下一个”m=”结束。

<media>：表示媒体类型。有"audio", "video", "application"（例白板信息）, "data"（不向用户显示的数据） 和"control"（描述额外的控制通道）。

<port>：媒体流发往传输层的端口。取决于c=行规定的网络类型和接下来的传送层协议：对UDP为1024-65535；对于RTP为偶数。

当分层编码流被发送到一个单播地址时，需要列出多个端口。方式如下： m=<media> <port>/<number of ports> <transport> <fmt list> 对于RTP，偶数端口被用来传输数据，奇数端口用来传输RTCP包。例： m=video 49170/2 RTP/AVP 31 端口49170和49171为第一对RTP/RTCP端口，49172和49173为第二对的端口。传输协议是RTP/AVP，媒体格式为31。

<transport>：传输协议，与c=行的地址类型有关。两种： RTP/AVP，表示Realtime Transport Protocol using the Audio/Video profile carried over UDP；UDP。

<fmt list>：媒体格式。对于音频和视频就是在RTP Audio/Video Profile定义的负载类型(payload type)。但第一个为缺省值，分为静态绑定和动态绑定：静态绑定即媒体编码方式与RTP负载类型有确定的一一对应关系，动态绑定即媒体编码方式（如时钟频率，音频信道数等）没有完全确定，需要进一步的属性说明（用rtpmap）。

分别举例如下：
静态绑定的例子：u_law的PCM编码单信道Audio，采样率8KHZ。在RTP Audio/Video profile中对应的payload type为0。即： m=audio 49232 RTP/AVP 0

动态绑定的例子：16位线形编码，采样率为16KHZ，假如我们希望动态RTP/AVP 类型98表示此此流，写法如下： m=video 49232 RTP/AVP 98 a=rtpmap:98 L16/16000/2

rtpmap（可选）
a=rtpmap:<payload type> <encoding name>/<clock rate>[/<encodingparameters>]

a=rtpmap:<负载类型><编码名>/<时钟速率>[/<编码参数>]

对于音频流，<编码参数>说明了音频的通道数。通道数默认缺省值为1。
对于视频流，现阶段没有<编码参数>。
m=audio 49230 RTP/AVP 96 97 98 a=rtpmap:96 L8/8000 a=rtpmap:97 L16/8000 a=rtpmap:98 L16/11025/2

在rtpmap中，实验性的编码方案也可以用。其格式名前一定为”X－”例：一种新的实验性的被称为GSMLPC的音频流，使用的动态负载类型为99。 m=video 49232 RTP/AVP 99 a=rtpmap:99 X-GSMLPC/8000 9．Suggested Attributes（可选） a=<TYPE>或 a=<TYPE>:<VALUES> a=framerate:<帧速率>//单位:帧/秒 a=lang:<语言标记>//会话描述的缺省语言或媒体描述的语言

注： 如果SDP语法分析器不能识别某一类型(Type),则整个描述丢失。 如果”a=”的某属性值不理解,则予以丢失此属性。 会话级的描述就是媒体级描述的。

````

```java
Session description

v= (protocol version)
o= (owner/creator and session identifier).
s= (session name)
i=* (session information)
u=* (URI of description)
e=* (email address)
p=* (phone number)
c=* (connection information - not required if included in all media)
b=* (bandwidth information)
z=* (time zone adjustments)
k=* (encryption key)
a=* (zero or more session attribute lines)

Time description
t= (time the session is active)
r=* (zero or more repeat times)

Media description
m= (media name and transport address)
i=* (media title)
c=* (connection information - optional if included at session-level)
b=* (bandwidth information)
k=* (encryption key)
a=* (zero or more media attribute lines)

```

## 强制 WebRTC 使用转发(relay)模式

[https://blog.csdn.net/foruok/article/details/72677338](https://blog.csdn.net/foruok/article/details/72677338)

webrtc 服务器[https://blog.csdn.net/bvngh3247/article/details/80746640](https://blog.csdn.net/bvngh3247/article/details/80746640)

NAThttps://www.cnblogs.com/whyandinside/archive/2010/12/08/1900492.html

## 基本网络概念

> 网关  
网关通常用来表示一个概念，作为内网和外网的接入点，一般我们称为网关。它的具体介质是路由器路由器  
是连接[因特网]、[广域网]的设备，它处于网络层，主要用来寻址。它会根据信道的情况自动选择和设定路由，以最佳路径，按前后顺序发送信号交换机  
在局域网（LAN）中，交换机类似于城市中的立交桥，它的主要功能是桥接其他网络设备（路由器、防火墙和无线接入点），并连接客户端设备（计算机、服务器、网络摄像机和 IP 打印机）。简而言之，交换机可以为网络上所有的不同设备提供一个中心连接点。

> TCP/UDP/HTTP/SOCKET  
tcp/udp 传输层  
http 是基于应用层，基于 tcp 协议  
socket 是 tcpip 中运输层 tcp 和 udp 协议中的一个实现寻址的重要实现websocket/http  
目的是取代 HTTP 在双向通信场景下的使用，而且它的实现方式有些也是基于 HTTP 的（WS 的默认端口是 80 和 443）相同点  
都是基于 TCP 的应用层协议。  
都使用 Request/Response 模型进行连接的建立。  
在连接的建立过程中对错误的处理方式相同，在这个阶段 WS 可能返回和 HTTP 相同的返回码。  
都可以在网络中传输数据。不同点  
WS 使用 HTTP 来建立连接，但是定义了一系列新的 header 域，这些域在 HTTP 中并不会使用。  
WS 的连接不能通过中间人来转发，它必须是一个直接连接。  
WS 连接建立之后，通信双方都可以在任何时刻向另一方发送数据。  
WS 连接建立之后，数据的传输使用帧来传递，不再需要 Request 消息。  
WS 的数据帧有序。

**webrtc 调试工具 chrome://webrtc-internals 的使用手册**

查看远端的视频编码

Read Stats From 改为 Legacy non-standard(callback-based) getstats api

ssrc_2181152470_recv (ssrc)

googCodecName 即可看到 vp8 还是 h264

````
音频统计数据
aecDivergentFilterFraction：TBD（后续会补全）

audioInputLevel：发送端采集的音频能量大小。

bitsSentPerSecond：每秒发送出去的比特数。

packetsSentPerSecond：每秒发送出去的音频包数。

googEchoCancellationQualityMin：TBD（后续会补全）

googEchoCancellationReturnLoss：TBD（后续会补全）

googEchoCancellationReturnLossEnhancement：TBD（后续会补全）

googResidualEchoLikelihood：Chrome 56中新增的，主要用来标识是否存在回声，范围为0 （没有回声）- 1（有回声），当值大于0.5时表明存在回声。

视频统计数据
bitsSentPerSecond：每秒发送出去的比特数，根据当前网络情况会进行动态调整。

framesEncoded：累计编码出来的视频帧数，没有异常情况的话会一直增长。

packetsLost：发送端从接收端发送过来的RTCP Receiver Report中得到的累积丢包数量，可以和googNacksReceived数据进行对照。

googRtt：Rtt全称为Round-trip time，是发送端从接受端发送过来的RTCP Receiver Report中得到的时间戳通过计算得到的往返时延。

packetsSentPerSecond：Chrome 56中新增的，每秒发送出去的视频包数量。

qpSum：发送端编码出的带有QP值的帧的数量，QP全称为Quantization Parameter。

googAdaptationChanges：发送端因为CPU的负载变化导致的分辨变高或者变低的次数，需要设置googCpuOveruseDetection。

googAvgEncodeMs：发送端平均编码时间，越小越好。

googEncodeUsagePercent：发送端（平均每帧编码时间）／（平均每帧采集时间），反应编码效率。

googFirsReceived：发送端收到的关键帧请求数量，FIR全称为Full Intra Request，一般来说在video conference模式下，有新的参与者进来会发出。

googPlisReceived：发送端收到的关键帧请求数量，PLI全称为Picture Loss Indication，一般来说在解码失败时会发出。

googNacksReceived：发送端收到的重传包请求数量，Nack全称为Negative ACKnowledgement可以和packetsLost数据进行对照。

googFrameHeightSent：发送端发送的分辨率高度，根据当前网络会进行动态调整。

googFrameWidthSent：发送端发送的分辨率宽度，根据当前网络会进行动态调整。

googFrameRateInput：发送端设置的初始帧率。

googFrameRateSent：发送端实际发送的帧率，根据当前网络会进行动态调整。
编辑于 2017-03-10

````

## android 编解码

````
软解码器：通常以OMX.google开头，或者不以OMX开头的也为软解码器
硬解码器：通常以OMX.[hardware_vendor]开头

````

````

高通软编解码
OMX.google.aac.decoder
OMX.google.amrnb.decoder
OMX.google.flac.decoder
OMX.google.g711.alaw.decoder
OMX.google.g711.mlaw.decoder
OMX.google.gsm.decoder
OMX.google.mp3.decoder
OMX.google.opus.decoder
OMX.google.raw.decoder
OMX.google.vorbis.decoder
OMX.google.aac.encoder
OMX.google.amrnb.encoder
OMX.google.amrwb.encoder
OMX.google.flac.encoder
OMX.google.h264.decoder
OMX.google.h263.decoder
OMX.google.hevc.decoder
OMX.google.mpeg4.decoder
OMX.google.vp8.decoder
OMX.google.vp9.decoder
OMX.google.h264.encoder
OMX.google.h263.encoder
OMX.google.mpeg4.encoder
OMX.google.vp8.encoder
OMX.google.aac.decoder
OMX.google.amrwb.decoder

c2.android.vp8.decoder - 2048
c2.android.vp8.encoder -2048
c2.android.vp9.decoder - 2048
c2.android.vp9.encoder -2048
OMX.qti.audio.decoder.flac
OMX.qti.video.decoder.divxsw
OMX.qti.video.decoder.divx4sw
OMX.qti.video.decoder.h263sw
OMX.qti.video.decoder.mpeg4sw
OMX.qti.video.decoder.vc1sw

````

````

高通硬解
OMX.qcom.video.decoder.avc - 264
OMX.qcom.video.decoder.hevc -265
OMX.qcom.video.decoder.mpeg2
OMX.qcom.video.decoder.vp8 -2304
OMX.qcom.video.decoder.vp9 -4320
高通硬编
OMX.qcom.video.encoder.heic
OMX.qcom.video.encoder.avc -h264
OMX.qcom.video.encoder.h263sw
OMX.qcom.video.encoder.hevc -h265
OMX.qcom.video.encoder.hevc.cq
OMX.qcom.video.encoder.mpeg4sw -720
OMX.qcom.video.encoder.vp8 -2304
海思硬编
OMX.hisi.video.encoder.avc
OMX.hisi.video.encoder.hevc
海思硬解
OMX.hisi.video.decoder.avc
OMX.hisi.video.decoder.hevc
OMX.hisi.video.decoder.mpeg2
OMX.hisi.video.decoder.mpeg4
OMX.hisi.video.decoder.vp8  -1088

````

判断是否为软解

````
frameworks/av/media/libstagefright/MediaCodecList.cpp

 bool MediaCodecList::isSoftwareCodec(const AString &componentName) {
    return componentName.startsWithIgnoreCase("OMX.google.")
            || componentName.startsWithIgnoreCase("c2.android.")
            || (!componentName.startsWithIgnoreCase("OMX.")
                    && !componentName.startsWithIgnoreCase("c2."));
}

````

相关文档

[https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/data/media_codecs_google_c2_video.xml](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/data/media_codecs_google_c2_video.xml)

## 获取手机最大解码数量

```java

public static void printMediaCodecInfo() {

    int CodecCount = 0;
    try {
        CodecCount = MediaCodecList.getCodecCount();
    }catch (Exception e) {
        Log.e(TAG, "#### Failed to get codec count!");
        e.printStackTrace();
        return;
    }

    for (int i = 0; i < CodecCount; ++i) {
        MediaCodecInfo info = null;
        try {
            info = MediaCodecList.getCodecInfoAt(i);
        } catch (IllegalArgumentException e) {
            Log.e(TAG, "Cannot retrieve decoder codec info", e);
        }
        if (info == null) {
            continue;
        }

        String codecInfo = "MediaCodec, name="+info.getName()+", [";

        for (String mimeType : info.getSupportedTypes()) {
            codecInfo += mimeType + ",";
            MediaCodecInfo.CodecCapabilities capabilities;
            try {
                capabilities = info.getCapabilitiesForType(mimeType);
            } catch (IllegalArgumentException e) {
                Log.e(TAG, "Cannot retrieve decoder capabilities", e);
                continue;
            }

            codecInfo += " max inst:"+capabilities.getMaxSupportedInstances()+",";

            String strColorFormatList = "";
            for (int colorFormat : capabilities.colorFormats) {
                strColorFormatList += " 0x" + Integer.toHexString(colorFormat);
            }
            codecInfo += strColorFormatList + "] [";
        }

        Log.w(TAG, codecInfo);
    }

    boolean bSupportHwVP8 = MediaCodecVideoEncoder.isVp8HwSupported();
    boolean bSupportHwVP9 = MediaCodecVideoEncoder.isVp9HwSupported();
    boolean bSupportHwH264 = MediaCodecVideoEncoder.isH264HwSupported();

    String webrtcCodecInfo = "WebRTC codec support: HwVP8=" + bSupportHwVP8 + ", HwVP9=" + bSupportHwVP9
            + ", Hw264=" + bSupportHwH264;

    if(bSupportHwH264) {
        webrtcCodecInfo += ", Hw264HighProfile=" + MediaCodecVideoEncoder.isH264HighProfileHwSupported();
    }

    Log.w(TAG, webrtcCodecInfo);
}

```

### 华为对 h264 的支持

```java
webrtc内部h264只支持两种 OMX.qcom. 和 OMX.Exynos.需改以下配置即可
HardwareVideoEncoderFactory.java

   private boolean isHardwareSupportedInCurrentSdkH264(MediaCodecInfo info) {
        if (H264_HW_EXCEPTION_MODELS.contains(Build.MODEL)) {
            return false;
        } else {
            String name = info.getName();
            return name.startsWith("OMX.qcom.") && VERSION.SDK_INT >= 19 || name.startsWith("OMX.Exynos.") && VERSION.SDK_INT >= 21 || name.startsWith("OMX.google.") && VERSION.SDK_INT >= 19;
        }
    }

```

## webrtc 媒体信息含义

[https://docs.google.com/document/d/1z-D4SngG36WPiMuRvWeTMN7mWQXrf1XKZwVl3Nf1BIE/edit#](https://docs.google.com/document/d/1z-D4SngG36WPiMuRvWeTMN7mWQXrf1XKZwVl3Nf1BIE/edit#) [https://w3c.github.io/webrtc-stats/](https://w3c.github.io/webrtc-stats/)

### webrtc 中的 SurfaceViewRender 及 EglRender 详解

[https://blog.csdn.net/blueair_ren/article/details/108163151](https://blog.csdn.net/blueair_ren/article/details/108163151) [https://blog.piasy.com/2018/05/24/WebRTC-Video-Native-Journey/index.html](https://blog.piasy.com/2018/05/24/WebRTC-Video-Native-Journey/index.html)

## 关于 H.264 profile-level-id

[https://blog.csdn.net/epubcn/article/details/102802108](https://blog.csdn.net/epubcn/article/details/102802108)

### webrtc 安卓屏幕旋转问题

[https://blog.csdn.net/epubcn/article/details/101451547](https://blog.csdn.net/epubcn/article/details/101451547)

## webrtc 修改带宽

[https://webrtc.org.cn/modify-sdp/](https://webrtc.org.cn/modify-sdp/)

### SDP Profile-level-id 解析

[https://blog.csdn.net/liang12360640/article/details/52096499](https://blog.csdn.net/liang12360640/article/details/52096499) ### sdp packetization-mode

````
packetization-mode:
表示支持的封包模式.
1 、packetization-mode 值为 0 时或不存在时, 必须使用单一 NALU 单元模式.
2、 packetization-mode 值为 1 时使用非交错(non-interleaved)封包模式.
3、 packetization-mode 值为 2 时使用交错(interleaved)封包模式.

````

### sdp

[https://www.cnblogs.com/chyingp/p/sdp-in-webrtc.html](https://www.cnblogs.com/chyingp/p/sdp-in-webrtc.html)

### h264 的支持

```java
./src/webrtc/sdk/android/api/org/webrtc/MediaCodecVideoEncoder.java
./src/webrtc/sdk/android/api/org/webrtc/MediaCodecVideoDecoder.java

private static final String[] supportedH264HwCodecPrefixes = {
    "OMX.qcom.", "OMX.Intel.", "OMX.Exynos."
    ,"OMX.Nvidia.H264."     /*Nexus 7(2012), Nexus 9, Tegra 3, Tegra K1*/
    ,"OMX.ittiam.video."    /*Xiaomi Mi 1s*/
    ,"OMX.SEC.avc."         /*Exynos 3110, Nexus S*/
    ,"OMX.IMG.MSVDX."       /*Huawei Honor 6, Kirin 920*/
    ,"OMX.k3.video."        /*Huawei Honor 3C, Kirin 910*/
    ,"OMX.hisi."            /*Huawei Premium Phones, Kirin 950*/
    ,"OMX.TI.DUCATI1."      /*Galaxy Nexus, Ti OMAP4460*/
    ,"OMX.MTK.VIDEO."       /*no sense*/
    ,"OMX.LG.decoder."      /*no sense*/
    //,"OMX.rk.video_decoder."/*Youku TVBox. our service doesn't need this */
    //,"OMX.amlogic.avc"      /*MiBox1, 1s, 2. our service doesn't need this */
};

```

### webbrtc 切换编解码

````
1、拷贝libwebrtc.jar并引用
2、as打开jar包里需要修改的文件MediaCodecVideoDecoderFactory.class，复制内容并新建文件到相同路径下;如：
java/org/webrtc/MediaCodecVideoDecoderFactory.java
3、修改MediaCodecVideoDecoderFactory代码内容如(过滤img硬解改为软解)：

    private boolean isSupportedCodec(MediaCodecInfo info, VideoCodecType type) {
        String name = info.getName();
        if (!MediaCodecUtils.codecSupportsType(info, type)) {
            return false;
        } else if (!checkScreenIsPhone(ContextUtils.getApplicationContext()) && name.contains("OMX.MS.VP8.Decoder")) {
            Log.d(TAG, "isSupportedCodec: 小米电视此解码器只支持2路");
            return false;
        }else if(name.contains("OMX.IMG")){
            Log.d(TAG, "isSupportedCodec: 过滤硬解");
            return  false;
        }
        else {
            return MediaCodecUtils.selectColorFormat(MediaCodecUtils.DECODER_COLOR_FORMATS, info.getCapabilitiesForType(type.mimeType())) == null ? false : this.isCodecAllowed(info);
        }
    }
4、编译
5、拷贝build/intermediates/javac/debug/classes/org/webrtc/MediaCodecVideoDecoderFactory.class
6、将以上文件拷贝到libwebrtc.zip中替换源文件，再改为.jar即可

````

### 获取手机支持的编解码信息

````
   if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
            MediaCodecList list = new MediaCodecList(MediaCodecList.REGULAR_CODECS);
            MediaCodecInfo[] supportCodes = list.getCodecInfos();
            Log.i(TAG, "解码器列表：");
            for (MediaCodecInfo codec : supportCodes) {
                if (!codec.isEncoder()) {
                    String name = codec.getName();
                    if (name.startsWith("OMX.google")) {
                        Log.i(TAG, "软解->" + name);
                    }
                }
            }
            for (MediaCodecInfo codec : supportCodes) {
                if (!codec.isEncoder()) {
                    String name = codec.getName();
                    if (!name.startsWith("OMX.google")) {
                        Log.i(TAG, "硬解->" + name);
                    }
                }
            }
            Log.i(TAG, "编码器列表：");
            for (MediaCodecInfo codec : supportCodes) {
                if (codec.isEncoder()) {
                    String name = codec.getName();
                    if (name.startsWith("OMX.google")) {
                        Log.i(TAG, "软编->" + name);
                    }
                }
            }
            for (MediaCodecInfo codec : supportCodes) {
                if (codec.isEncoder()) {
                    String name = codec.getName();
                    if (!name.startsWith("OMX.google")) {
                        Log.i(TAG, "硬编->" + name);
                    }
                }
            }
        }

````

### webrtc 安卓源码

[https://webrtc.googlesource.com/src/+/refs/heads/main/sdk/android/api/org/webrtc](https://webrtc.googlesource.com/src/+/refs/heads/main/sdk/android/api/org/webrtc)

### 华为解码 H264-720p 分辨率问题

````
AndroidVideoDecoder.java中deliverDecodedFrame方法增加：
if ((long)decodeTimeMs > 200L) {
Logging.e("AndroidVideoDecoder", "Very high decode time: " + decodeTimeMs + "ms. Q size: . Might be caused by resuming H264 decoding after a pause.");
decodeTimeMs = 200;
}

````

### 华为平板h264失败

````
## webrtc编解码过程
DefaultVideoEncoderFactory - createEncoder ：
华为平板softwareEncoder是null，在HardwareVideoEncoderFactory中执行isHardwareSupportedInCurrentSdkH264
除了华为平板其他设备：
DefaultVideoDecoderFactory - createDecoder
HardwareVideoDecoderFactory-
MediaCodecVideoDecoderFactory - createDecoder
AndroidVideoDecoder -
后执行：
DefaultVideoEncoderFactory --

    private boolean isHardwareSupportedInCurrentSdk(MediaCodecInfo info, VideoCodecMimeType type) {
        if (VERSION.SDK_INT >= 29) {
        //大于android10的系统都进入此方法
        //返回true,支持硬件加速的都判断为支持当前编码？比如华为只有omx.hisi会进入这个方法
            return info.isHardwareAccelerated();
        } else {
            switch(type) {
                case VP8:
                    return this.isHardwareSupportedInCurrentSdkVp8(info);
                case VP9:
                    return this.isHardwareSupportedInCurrentSdkVp9(info);
                case H264:
                //华为平板版本android9，所以进入此方法
                    return this.isHardwareSupportedInCurrentSdkH264(info);
                case AV1:
                    return false;
                default:
                    return false;
            }
        }
    }

````

### 各型号手机编解码大全

[https://videoprocessing.ai/benchmarks/mobile-video-codec-benchmark.html](https://videoprocessing.ai/benchmarks/mobile-video-codec-benchmark.html)

- https://juejin.cn/post/7232872175647473722 固定分辨率
