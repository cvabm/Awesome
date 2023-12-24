# react native常见问题

slug: react-native-problem
status: Published
tags: react
type: Post

## `null is not an object (evaluating ‘_RNGestureHandlerModule.default.Direction’)`

起因：使用 RN 跨平台开发时使用 react-navigation 组件，需要链接原生库

解决：react-native link

## `Could not get unknown property ‘mergeResourcesProvider’`

```
解决办法：
更新gradle版本和gradle build tool版本
gradle最低为 4.10.1+ ，插件最低为 3.3.0 - 3.3.2
```

## `解决 React Native 生成 released apk 图片不显示`

[https://segmentfault.com/a/1190000008528838](https://segmentfault.com/a/1190000008528838)

## `运行时报错ENOENT: no such file or directory, open app/src/main/AndroidManifest.xml`

默认主 module 名称为 app，想自定义启动 module，命令为：

react-native run-android –appFolder (appFolder 为自己定义的 module 名)

## `启动程序时报错，手动编译`

react-native bundle –platform android –dev false –entry-file index.js –bundle-output android/app/src/main/assets/index.android.bundle –assets-dest android/app/src/main/res/

## `启动白屏，清理缓存`

进入 android 目录，执行 gradlew.bat clean。再重新启动

## `跨域问题`

1、新建 chrome 快捷方式

2、右击 -快捷方式 - 属性 - 目标 -

```
"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --disable-web-security --user-data-dir=c:/Hello
```

### `npm WARN deprecated core-js@2.6.11: core-js@<3 is no longer maintained and not recommended for usage due to the number of issues. Please, upgrade your dependencies to the actual version of core-js@3.`

换 vpn 是网络问题

### `rn 编译报错 Android build failures No matching variant of com.facebook.react:react-native:0.71.0-rc.0 was found`

https://github.com/facebook/react-native/issues/35210

### `rn 分割线不显示或粗细不均匀`

```
borderBottomColor: '#e0e0e0',
borderBottomWidth: 1,
```

## `Error: Metro ‘Bundler’ process exited with code 1`

这个错误是node不同版本语法问题导致,解决办法

If you are running on windows you can try the solutions provided in this thread on github.

Solution from github that seems to work:

```
Got this issue today on windows, but don't need to downgrade node, just as discussed on stackoverflow just need to change some hashes on your project:

\node_modules\metro-config\src\defaults\blacklist.js

var sharedBlacklist = [
  /node_modules[/\\]react[/\\]dist[/\\].*/,
  /website\/node_modules\/.*/,
  /heapCapture\/bundle\.js/,
  /.*\/__tests__\/.*/
];

```

change to:

```
var sharedBlacklist = [
  /node_modules[\/\\]react[\/\\]dist[\/\\].*/,
  /website\/node_modules\/.*/,
  /heapCapture\/bundle\.js/,
  /.*\/__tests__\/.*/
];
```

## `Failed to transform file ‘xxx.aar’ to match attributes`

查看是否有中文名称的文件