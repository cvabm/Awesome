# reagt-native依赖包

slug: react-native-plugin
status: Published
tags: react
summary: 添加依赖、发布npm
type: Post

## 发布 npm

1、注册：

```
打开网站：https://www.npmjs.com/，点击页面右上角sign up打开注册页面：
注意： Full Name、Password和Public Email 注册以后可以修改，Username注册后不可修改。
注册后需要去邮箱中确认一下。

npm config get registry # 查看当前镜像源
设置本地npm镜像为官方
npm set registry https://registry.npmjs.org/

命令行登录npm账号
npm login
依次输入username、password、Email
提示Enter one-time password from your authenticator app:
输入npm上2fa增加的很长的那串验证秘钥

```

2、新建测试项目：

```
npm install -g react-native-create-library

react-native-create-library mytestlib123 --platforms android,ios

npm publish
提示：This operation requires a one-time password：
输入验证器里的6位数密码

```

3、其他项目使用：

```
npm install

import * as RNMytestlib123  from 'react-native-mytestlib123';

RNMytestlib123.testMy()

```

## 发布 jitpack

## 步骤 1: 新建 Lib 工程

在 AndroidStudio 中新建 Android Library 工程,结构如下

![http://upload-images.jianshu.io/upload_images/4048192-755470ecd25ab04a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240](http://upload-images.jianshu.io/upload_images/4048192-755470ecd25ab04a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 解释:

1.在项目的 build.gradle 的 buildscript 添加 jitpack 编译插件

```
 buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.1.3'
        //添加jitpack依赖
        classpath 'com.github.dcendents:android-maven-gradle-plugin:1.5'
    }
}
```

2.在 library 的 build.gradle 中添加 jitpack 配置信息

```
//启用Jitpack 插件
apply plugin: 'com.github.dcendents.android-maven'

//设置Jitpack发布的Group
//我的github账号是helen-x, 对应我的group就是com.github.helen-x
group='com.github.helen-x'

```

## 步骤 2: Github 上发布代码

### 1.上面代码发布到 Github

### 2.发布代码(Release/TAG)

找到对应项目,进入 release 页面

![http://upload-images.jianshu.io/upload_images/4048192-97d738c667e41eaa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240](http://upload-images.jianshu.io/upload_images/4048192-97d738c667e41eaa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

进入 release 以后,进行代码发布. 发布的时候可以用 Releases 也可以用 Tags.

![http://upload-images.jianshu.io/upload_images/4048192-1896d6c6c531bfed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240](http://upload-images.jianshu.io/upload_images/4048192-1896d6c6c531bfed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

填写发布信息后,就可以发布了

![http://upload-images.jianshu.io/upload_images/4048192-38f812569de24fd6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240](http://upload-images.jianshu.io/upload_images/4048192-38f812569de24fd6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 步骤 3: Jitpack 发布

进入[Jitpack link](https://jitpack.io/?spm=a2c6h.12873639.article-detail.5.1c0e6fe6SmYs4M).

> 1.填写仓库名称 2.搜索 3.使用“Get”, 发布就成功啦~~
> 

![http://upload-images.jianshu.io/upload_images/4048192-4e9734e3520ba9f6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240](http://upload-images.jianshu.io/upload_images/4048192-4e9734e3520ba9f6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

发布成功后,会列出仓库的地址信息, 别人利用这个坐标就可以用我们的开源库啦. 比如,我的 demo 发布后的地址是: `com.github.helen-x:JitpackReleaseDemo:0.1`

## 步骤 4: 使用我们的开源库

1.在 build.gradle 中加入 Jitpack 仓库

```
allprojects {
        repositories {
            ...
            maven { url 'https://jitpack.io' }
        }
    }
```

2.使用我们开源库

```
    dependencies {
            compile 'com.github.helen-x:JitpackReleaseDemo:0.1'
    }
```

拓展 可以在仓库的 readme.md 中加入

![https://jitpack.io/v/helen-x/JitpackReleaseDemo.svg](https://jitpack.io/v/helen-x/JitpackReleaseDemo.svg)

就会自动会有一个 Jitpack 的 bar,效果如下,瞬间显得很高端有木有~

## 常用依赖：

react-native-webrtc react-native-incall-manager react-native-permissions React Native Vector Icons react-native-orientation-locker

react-native-device-info react-native-image-picker react-native-video react-native-fs react-native-camera react-native-aws3

图标库 https://atlassian.design/components/icon/icon-explorer https://github.com/bytedance/iconpark https://github.com/oblador/react-native-vector-icons https://github.com/react-icons/react-icons https://atlassian.design/components 设计库： @mui/material

“@react-native-community/datetimepicker”: “^3.0.1”, “@react-native-community/masked-view”: “^0.1.10”, “@react-native-community/netinfo”: “^5.9.5”, “@react-native-community/slider”: “^3.0.3”, “@react-navigation/bottom-tabs”: “^5.8.0”, “@react-navigation/material-top-tabs”: “^5.2.16”, “@react-navigation/native”: “^5.7.3”, “@react-navigation/stack”: “^5.9.0”, “axios”: “^0.19.2”, “babel-plugin-flow-react-proptypes”: “^9.1.1”, “crypto-js”: “3.1.9-1”, “hermes-engine”: “^0.5.2-rc1”, “json-bigint”: “^1.0.0”, “moment”: “^2.27.0”, “prop-types”: “^15.6.0”, “react”: “^16.13.1”, “react-dom”: “^16.13.1”, “react-native”: “0.63.5”, “react-native-amap3d”: “^3.1.3”, “react-native-audio”: “^4.3.0”, “react-native-config”: “1.3.3”, “react-native-contacts”: “^5.2.5”, “react-native-device-info”: “^5.6.3”, “react-native-draggable-flatlist”: “^3.1.2”, “react-native-easy-grid”: “^0.2.2”, “react-native-easy-loading”: “^1.0.6”, “react-native-easy-toast”: “^2.0.0”, “react-native-elements”: “^2.1.0”, “react-native-fs”: “^2.18.0”, “react-native-gesture-handler”: “^1.7.0”, “react-native-gifted-chat”: “^0.16.3”, “react-native-idle-timer”: “^2.1.6”, “react-native-image-crop-picker”: “^0.32.2”, “react-native-inback-timer-ios”: “^0.1.0”, “react-native-incall-manager”: “^4.0.0”, “react-native-md5”: “^1.0.0”, “react-native-modal-dropdown”: “^1.0.2”, “react-native-reanimated”: “^1.10.1”, “react-native-root-siblings”: “^3.2.2”, “react-native-safe-area-context”: “^3.1.1”, “react-native-screens”: “^2.9.0”, “react-native-sound”: “^0.11.1”, “react-native-storage”: “^1.0.1”, “react-native-system-setting”: “1.7.6”, “react-native-tab-view”: “^2.15.0”, “react-native-theming”: “^1.0.21”, “react-native-video”: “^5.2.0”, “react-native-webrtc”: “1.100.1”, “react-native-webview”: “^11.18.2”, “uuid”: “3.4.0”

react-native-webrtc：提供 WebRTC 的基础功能，包括媒体设备管理、信令传输和数据通道等功能。

react-native-incall-manager：用于管理 Android 和 iOS 设备的通话状态、通话模式和音频路由等功能。

react-native-callkeep：提供了一套标准的呼叫 UI 界面，可以让用户在接听或拒接电话时获得更好的用户体验。

react-native-permissions

react-native-default-preference：SharedPreferences

react-native-dialog：

react-native-device-info：用于获取设备信息，如设备型号、操作系统版本等。

react-native-image-picker：用于从设备的相册或摄像头中选择图片或视频。

react-native-video：用于播放本地或远程视频。

react-native-video-thumbnail：用于从本地或远程视频中获取缩略图。

react-native-udp：用于通过 UDP 协议进行数据传输。

react-native-background-task：用于在后台运行任务，如网络请求、数据存储等。

react-native-fs：用于在本地存储文件，如音频、视频等。

react-native-camera：用于在应用程序中调用摄像头进行拍照或录制视频。

react-native-webrtc-streamer：用于将本地摄像头或屏幕共享的视频流传输到远程 Peer，支持多路媒体流混合。

react-native-aws3：用于将视频或音频文件上传到 AWS S3 存储桶中。

react-native-audio-recorder-player：用于录制和播放本地音频。

界面：

React Native Elements：这是一个流行的 UI 组件库，包含了丰富的组件和主题，可以帮助开发者快速构建漂亮、易用的界面。

React Native Paper：这是一个 Material Design 风格的组件库，提供了大量的基础组件和交互式组件，可以用于创建符合 Material Design 风格的应用程序。

React Native Vector Icons：这是一个矢量图标库，包含了超过 3000 个矢量图标，可以用于创建漂亮的图标和按钮。

React Navigation：这是一个流行的导航组件库，提供了丰富的导航组件和 API，可以帮助开发者创建复杂的导航结构和交互效果。

React Native Gifted Chat：这是一个聊天组件库，提供了丰富的聊天组件和交互效果，可以用于创建聊天室和消息通讯应用程序。

NativeBase：这是一个 UI 组件库，提供了超过 300 个 UI 组件和主题，可以用于创建漂亮、易用的界面。

Shoutem UI：这是一个 UI 组件库，提供了丰富的 UI 组件和主题，可以帮助开发者快速构建漂亮、易用的应用程序。

Ant Design Mobile：这是一个 UI 组件库，提供了丰富的 UI 组件和交互式组件，可以用于创建符合 Ant Design 风格的应用程序。

React Native Material Kit：这是一个 Material Design 风格的组件库，提供了丰富的基础组件和交互式组件，可以用于创建符合 Material Design 风格的应用程序。

React Native UI Kitten：这是一个 UI 组件库，提供了丰富的 UI 组件和主题，可以用于创建漂亮、易用的应用程序。