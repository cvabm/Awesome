# java_net

slug: java_net
status: Published
tags: java
type: Post

[[toc]]

## 网络

### get 和 post 的区别

```
get和post虽然本质都是tcp/ip，但两者除了在http层面外，在tcp/ip层面也有区别。

get会产生一个tcp数据包，post两个

具体就是：

get请求时，浏览器会把headers和data一起发送出去，服务器响应200（返回数据），
post请求时，浏览器先发送headers，服务器响应100 continue，浏览器再发送data，服务器响应200（返回数据）。
再说一点，这里的区别是specification（规范）层面，而不是implementation（对规范的实现）
```

### frp 官方

[https://github.com/fatedier/frp](https://github.com/fatedier/frp)

### frpc 内网穿透

1、android 端编译流程：

https://github.com/FrpcCluster/frpc-Android/blob/master/Compile_zh.md [https://github.com/mainfunx/frpc_android](https://github.com/mainfunx/frpc_android)

### frp 编译

```

-----------------------------

编译Android-SDK环境指南( 所有操作均在root用户下执行)
安装 go
[root@localhost ~]# wget https://dl.google.com/go/go1.14.14.linux-amd64.tar.gz      #下载go1.10.x安装包
[root@localhost ~]# tar -zxvf go1.14.14.linux-amd64.tar.gz                                          #解压
[root@localhost ~]# mv go /usr/local/                                                             #移动运行目录

[root@localhost ~]# vi /etc/profile                                                               #添加系统变量

export GOROOT=/usr/local/go
export GOBIN=/usr/local/go/bin
export PATH=$PATH:$GOBIN:$JAVA_HOME/bin
export GOPATH=~/go
export ANDROID_HOME=~/go/android-sdk-linux

[root@localhost ~]# source /etc/profile                                                           #生效
[root@localhost ~]# go version                                                                    #验证安装是否成功
go version go1.14.14 linux/amd64
安装 gomobile 安卓开发环境
[root@localhost ~]# mkdir -p /usr/local/go/src/golang.org/x                                       #创建golang目录,或存放~/go/src/golang.org/x(有时会被墙所以手动)
[root@localhost ~]# cd /usr/local/go/src/golang.org/x                                             #进入目录

//github连接失败情况下，使用git clone https://github.com.cnpmjs.org/golang/mobile.git镜像来下载

[root@localhost x]# git clone https://github.com/golang/mobile.git                                #克隆库
[root@localhost ~]# go build golang.org/x/mobile/cmd/gomobile                                     #编译
[root@localhost ~]# go install golang.org/x/mobile/cmd/gomobile                                   #安装
[root@localhost ~]# gomobile init -v
[root@localhost ~]# gomobile version                                                              #验证
gomobile version +5704e18 Mon Jan 22 17:02:51 2018 +0000 (android); androidSDK=

安装 java jdk
ubuntu
[root@localhost ~]# apt-get install openjdk-8-jdk                                                 #ubuntu下安装
[root@localhost ~]# java -version
                                                               #验证
安装 android ndk
[root@localhost ~]# wget http://dl.google.com/android/repository/android-ndk-r20b-linux-x86_64.zip  #下载源码包
[root@localhost ~]# unzip android-ndk-r20b-linux-x86_64.zip                                              #解压
[root@localhost ~]# gomobile init -ndk ~/android-ndk-r20b                                                #安装

可能要修改ndk环境路径
ANDROID_NDK_HOME=..\android-sdk\ndk\20.0.5594570
export ANDROID_NDK_HOME=$ANDROID_HOME/ndk/21.3.6528147

安装 android sdk
[root@localhost ~]# wget http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz                      #下载
[root@localhost ~]# tar -xvzf android-sdk_r24.4.1-linux.tgz                                              #解压
[root@localhost ~]# mv android-sdk-linux ~/go/                                                           #移动到用户目录下的go目录
[root@localhost ~]#  ~/go/android-sdk-linux/tools/android update sdk -u                                  #安装(请耐心等待)
[root@localhost ~]# gomobile version                                                                     #验证
gomobile version +92f3b9c Wed Oct 10 16:34:05 2018 +0000 (android); androidSDK=/root/go/android-sdk-linux/platforms/android-28

创建frp工程
[root@localhost ~]# mkdir -p /usr/local/go/src/github.com/fatedier                                      #创建项目目录，或存放~/go/src/github.com/fatedier
[root@localhost ~]# wget https://github.com/fatedier/frp/archive/v0.35.1.tar.gz                         #拷贝0.13.0 frp源码
[root@localhost ~]# tar -xzvf v0.35.1.tar.gz -C /usr/local/go/src/github.com/fatedier/                  #解压至目录
[root@localhost ~]# cd /usr/local/go/src/github.com/fatedier/                                           #切换目录
[root@localhost fatedier]# mv frp-0.35.1 frp                                                            #应环境更名
[root@localhost ~]# cd /usr/local/go/src/github.com/fatedier/frp/cmd/frpc                               #切换目录

编辑源文件(github.com/fatedier/frp/cmd/frpc/sub/root.go)
......

90 - err := runClient(cfgFile)
90 + err := RunClient(cfgFile)
......

172 - func runClient(cfgFilePath string) (err error) {
172 + func RunClient(cfgFilePath string) (err error) {

编辑源文件(github.com/fatedier/frp/cmd/frpc/main.go)
// Copyright 2016 fatedier, fatedier@gmail.com
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at
//
//     http://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

package frpclib

import (
    "github.com/fatedier/frp/cmd/frpc/sub"

    "github.com/fatedier/golib/crypto"
)

func main() {
    crypto.DefaultSalt = "frp"

    sub.Execute()
}

func Run(cfgFilePath string) {
    crypto.DefaultSalt = "frp"

    sub.RunClient(cfgFilePath)
}

编译库
[root@localhost ~]# gomobile bind -target=android github.com/fatedier/frp/cmd/frpc                      #编译(不报错的情况)
[root@localhost ~]# ls
frpclib.aar  frpclib-sources.jar  main.bak  main.go
Android SDK在线更新镜像服务器
http://mirrors.zzu.edu.cn/android/repository/
sdk
http://tools.android-studio.org/index.php/sdk

ld谷歌
http://blog.csdn.net/shuzfan/article/details/52690554

---------------------------------------

gomobile 正确安装姿势

边城刀客 2020-08-19 11:38:55  253  收藏 1
分类专栏： GO
版权
0x01.下载代码

git clone https://github.com/golang/mobile.git
git clone https://github.com/golang/mod.git
git clone https://github.com/golang/xerrors.git
git clone https://github.com/golang/tools.git
或执行下面的命令（会自动下载到 $GOPATH/src/github.com 路径下）

go get github.com/golang/mobile
go get github.com/golang/mod
go get github.com/golang/xerrors
go get github.com/golang/tools
0x02. 复制到文件夹

将下载的代码复制到如下路径（没有就新建一个）：

$GOPATH/src/golang.org/x/
0x03. 设置go包管理代理地址

go包管理国内无法访问 proxy.golang.org 。设置代理地址： https://goproxy.cn

go env -w GOPROXY=https://goproxy.cn
0x04. 编译安装gobind

go get golang.org/x/mobile/cmd/gobind
执行命令后，$GOPATH\bin 目录下自动产生文件 gobind.exe

0x05. 编译安装gomobile

go get golang.org/x/mobile/cmd/gomobile
执行命令后，$GOPATH\bin 目录下自动产生文件 gomobile.exe

export GOPROXY=https://goproxy.io
go get -u -v golang.org/x/mobile/cmd/gomobile

mkdir -p $GOPATH/src/golang.org/x
cd $GOPATH/src/golang.org/x
git clone https://github.com/golang/sys.git

```

## frp 改名

```jsx
全局替换
命令改为gomobile bind -target=android.github.com/fatedier/sp/cmd/spc
```