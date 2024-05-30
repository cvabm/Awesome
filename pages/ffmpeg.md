# ffmpeg

slug: ffmpeg
status: Published
tags: other
summary: ffmpeg常用命令
type: Post

- 将本地mp4文件推流到rtsp
`ffmpeg -re -i 720.mp4 -c:v copy -c:a copy -f rtsp rtsp://localhost:8554/live`
- 将本地mp4文件推流到rtsp
`ffmpeg -re -stream_loop -1 -i .\\720.mp4 -vcodec libx264 -acodec aac -f flv rtmp://127.0.0.1:1935/live/hls`
- ffplay半屏播放
`ffplay -vf "scale=iw/2:ih/2" http://samples.mplayerhq.hu/V-codecs/h264/interlaced_crop.mp4`
- h264 ->rtp
`ffmpeg -re -i d:\videos\1080P.264 -vcodec copy -f rtp rtp://127.0.0.1:1234>test_rtp_h264.sdp`
`ffplay -protocol_whitelist "file,udp,rtp" -i test_rtp_h264.sdp`
- h264 -> ts
`ffmpeg -re -i d:\videos\1080P.264 -vcodec copy -f rtp_mpegts rtp://127.0.0.1:1234`
参考：https://zhuanlan.zhihu.com/p/450527182

### ffmpeg使用

* List Devices

```bash
ffmpeg -list_devices true -f dshow -i dummy
ffmpeg -hide_banner -devices
```

* Start Recording Camera (AVI Format)

```lua
ffmpeg -f dshow -i video="USB2.0 PC CAMERA" -c:v libx264 -preset ultrafast -qp 0 output.avi
ffmpeg -f dshow -i video="USB2.0 PC CAMERA" -c:v h464 -preset ultrafast -qp 0 output.avi
ffmpeg -f dshow -i video="USB2.0 PC CAMERA" -c:v h464 -preset medium output.avi
```

* Screen Recording (Requires FFmpeg with x11grab)

```csharp
ffmpeg -f x11grab -framerate 25 -video_size 1366x768 -i :0.0 -c:v libx264 -preset ultrafast out.mp4 ffmpeg -f x11grab -framerate 25 -video_size 1366x768 -i :0.0 -c:v libx264 -preset ultrafast out.mp4
```

* 其他

```bash
ffplay -vf "scale=iw/2:ih/2" your_video.mp4

ffprobe -v error -select_streams v:0 -show_entries stream=width,height,codec_name,bit_rate,duration your_h264_file.mp4 

ffprobe -v error -show_streams -show_format out.h264

ffmpeg -re -i 720.mp4 -c:v copy -c:a copy -f rtsp rtsp://localhost:8554/live

ffplay -vf "scale=iw/2:ih/2" https://iptv.luas.edu.cn/liverespath/c70d81eefb04fef7777c2a5aab4ddc9459ce4246/0baa43f537-0-0-5bc4eda6a2031a1140906b86d867a79e/index.m3u8

ffplay -vf "scale=iw/2:ih/2" http://samples.mplayerhq.hu/V-codecs/h264/interlaced_crop.mp4

ffmpeg -re -stream_loop -1 -i .\720.mp4 -vcodec libx264 -acodec aac -f flv  rtmp://127.0.0.1:1935/live/hls              
            
```
```
查看支持的编解码器（也就是-vcodec后面可以接的参数）:
命令：ffmpeg -codecs > codec.txt


查看支持的封装格式（也就是-f后面可以接的参数）
命令：ffmpeg -formats > formats.txt

查看支持的滤镜（也就是-vf后面可以接的参数）:
命令：ffmpeg -filters > filters.txt
```
