### RTP/H264开源项目
Android端的：
- https://github.com/qfsun/Jrtplib4Android 
- https://github.com/zhuohengfeng/Camera2Rtmp camera->rtmp
- https://github.com/dourgulf/CameraStreaming camera->rtmp
- https://github.com/JeffreyLau/AndroidRTSPLib camera/screen/mp4_file -> rtsp
- https://github.com/pedroSG94/RootEncoder 推送android摄像头/屏幕共享到RTMP, RTSP, SRT and UDP(没有RTP)
- https://github.com/Consti10/LiveVideo10ms 播放RTP或RAW中的udp的h264
- https://github.com/xcy396/MediaCodecDemo 使用 MediaCodec、jlibrtp 实现实时视频通话
- https://github.com/ChangeStrong/AndroidDemo 将摄像头yuv转H264
- https://github.com/mjlong123123/VideoRecorder 录屏发送到rtp，没验证过
- https://github.com/TomAdd/RTPServerDemo android端
- https://github.com/lxz2014/rtp_h264 android端，只编不发
- https://github.com/junerver/TestCaptureAndRecord websoket收发
- https://github.com/niezhiyang/TouPing websoket收发
其他  
- https://github.com/licaibiao/v4l2_video_audio_encode_live c++
- https://github.com/tong123/rtp_stream
- https://github.com/tinydigger/RTPH264Streaming
- https://github.com/MontaukLaw/hisiv3518e
- https://github.com/z80020100/RKModules
- https://github.com/yundiantech/ScreenShare
### RTP开源库
- ORTP c
- JRTPLIB c++
- jlibrtp java

### B帧
官方的profile配置不管用  
https://developer.android.com/media/optimize/sharing?authuser=1&hl=zh-cn#b-frames_and_encoding_profiles
```
format.setInt32(KEY_PROFILE, AVCProfileHigh);
format.setInt32(KEY_LATENCY, 1);
```
### 调试
- vlc播放rtp流
  -  新建文件11.sdp，内容如下，用vlc打开即可播放：
```
m=video 6666 RTP/AVP 96
a=rtpmap:96 H264
a=framerate:20
c=IN IP4 10.166.10.8
```
### mediacodec
- 创建编解码器的两种方式
  - `MediaCodec.createEncoderByType("video/avc")`
  - `MediaCodec.createByCodecName("OMX.Nvidia.h264.encoder")`
##   udp/h264发送
- udp不能发送大于1472字节数据,一般设为1400
- 先发sps\pps
- 通过sps查看视频分辨率
```
.000 0011  1100 .... = pic_width_in_mbs_minus1: 59
.... 0000  0101 101. = pic_height_in_map_units_minus1: 44
```
- `X = (59+1)*16 = 960，Y = (44+1)*16 = 720`

  
