## GSYVideoPlayer 使用

#### 倍速播放

1、如何文件无音频，IjkPlayerManager 无法倍速，需改为其他两种：

```
PlayerFactory.setPlayManager(Exo2PlayerManager.class);
或
PlayerFactory.setPlayManager(SystemPlayerManager.class);

然后再调用：
videoPlayer.setSpeedPlaying(2.0f,false);
```

### 增加 pcm_mulaw 支持

`echo -e 'export COMMON_FF_CFG_FLAGS="$COMMON_FF_CFG_FLAGS --enable-decoder=pcm_mulaw"' >> ./module-default.sh`

### github action 编译脚本

`https://github.com/cvabm/ijkplayer-autobuild/blob/master/.github/workflows/run_on_stared.yml`

### 播放rtsp设置
只要以下配置，其他不要加
```
PlayerFactory.setPlayManager(IjkPlayerManager.class);
   VideoOptionModel videoOptionModel = new VideoOptionModel(IjkMediaPlayer.OPT_CATEGORY_FORMAT, "rtsp_transport", "tcp");
        list.add(videoOptionModel);
		GSYVideoManager.instance().setOptionModelList(list);
```