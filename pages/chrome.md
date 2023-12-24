# chrome

date: October 30, 2023
slug: chrome
status: Published
tags: web
type: Post

### 卸载APP

`chrome://apps`

### chrome 删除某一个网站的缓存

F12 - local storage - clear all

打开开发者工具（F12），选择 Network——Disable cache 即可。需要清除某网站缓存时 F12 打开开发者工具就会自动清除这个网站的缓存，而不必清除所有网站的缓存了。

### chrome 书签同步设置

chrome://sync/

about - getUpdates

### chrome 隐藏插件项

[chrome://sync-internals/](chrome://sync-internals/)

chrome://downloads/

下载记录

chrome://webrtc-internals/

查看 webrtc 信息

chrome://extensions/

扩展管理

chrome://flags/

试验性功能

chrome://history/

历史记录

### chrome 浏览器提示您还没有安装 flash 播放器

[https://jingyan.baidu.com/article/36d6ed1f833ba31bcf4883e1.html](https://jingyan.baidu.com/article/36d6ed1f833ba31bcf4883e1.html)

### 快捷键

`ctrl L` 会选中地址栏内的文本，重新输入

[https://www.runoob.com/w3cnote/google-chrome-shortcuts.html](https://www.runoob.com/w3cnote/google-chrome-shortcuts.html)

### chrome 常用插件

常用

vysor：电脑控制手机（adb）

chromeadb

易撤销（历史关闭助手）

谷歌访问助手

[adblock plus](https://chrome.google.com/webstore/detail/adblock-plus-free-ad-bloc/cfhdojbkjhnklbpkdaibdccddilifddb)

[谷歌翻译](https://chrome.google.com/webstore/detail/google-translate/aapbdbdomjkkjkaonfhkkikfgjllcleb)

[User-Agent Switcher for Chrome](https://chrome.google.com/webstore/detail/djflhoibgkdhkhhcedjiklpkjnoahfmg)

[Sourcegraph](https://chrome.google.com/webstore/detail/sourcegraph/dgjhfomjieaadpoljlnidmbgkdffpack)

[Search by Image (by Google)](https://chrome.google.com/webstore/detail/search-by-image-by-google/dajedkncpodkggklbegccjpmnglmnflm)

[JSON-handle](https://chrome.google.com/webstore/detail/json-handle/iahnhfdhidomcpggpaimmmahffihkfnj)

[Fatkun 图片批量下载](https://chrome.google.com/webstore/detail/fatkun-batch-download-ima/nnjjahlikiabnchcpehcpkdeckfgnohf)

[easy-auto-refresh](https://chrome.google.com/webstore/detail/easy-auto-refresh/aabcgdmkeabbnleenpncegpcngjpnjkc)

[scrcpy](https://github.com/Genymobile/scrcpy)电脑控制手机（adb）

[Clear Cache](https://chrome.google.com/webstore/detail/clear-cache/cppjkneekbjaeellbfkmgnhonkkjfpdn)

devices 页面

```

chrome://inspect/#devices

```

地址栏显示完整 url

```

在地址栏右键 - 总是显示完成url

```

### 显示网址最后更新时间

`console.log(document.lastModified)`