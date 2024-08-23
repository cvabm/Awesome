# server

slug: server
status: Published
tags: other
summary: 后台服务器
type: Post

## 腾讯云搭建网页

```
$ ssh root@100.2.3.4

# 安装
$ yum install nginx -y

# 启动
$ nginx

# 关闭
$ nginx -s stop

# 重启
$ nginx -s reload

文件一般放在/data/wwww目录下
vim /etc/nginx/nginx.conf

server {
    listen       80;
    server_name  _;
    root         /data/www;

    # Load configuration files for the default server block.
    include /etc/nginx/default.d/*.conf;

    location / {
    }

    error_page 404 /404.html;
    location = /40x.html {
    }

    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
    }
}

把网页文件放到路径下

mkdir /data/www
touch /data/www/index.html
index.html写点内容
```

### linux运维

`cat /proc/version`

Linux系统分为两种：

1.[RedHat](https://so.csdn.net/so/search?q=RedHat&spm=1001.2101.3001.7020)系列：Redhat、Centos、Fedora等

2.[Debian](https://so.csdn.net/so/search?q=Debian&spm=1001.2101.3001.7020)系列：Debian、Ubuntu等

RedHat系列的包管理工具是[yum](https://so.csdn.net/so/search?q=yum&spm=1001.2101.3001.7020)

Debian系列的包管理工具是apt-get

```
可以查看根目录下的内容
ls /

详细的信息
ls -lh /

显示/root的全部内容，包括隐藏文档：
-A选项可以显示出目录中包含的隐藏文档
ls -A /root
cp命令用于复制文档，当复制多个文档时，逐一列出源文档的路径，并将目标路径作为最后一个参数即可
cp /etc/passwd /etc/resolv.conf /opt/test

将/home目录复制到/opt/test目录下 ：
cp命令复制目录时必须加上-r选项
cp -r /home /opt/test

使用 rpm 本地安装软件包vsftpd：
rpm命令用于安装软件包（默认不显示安装过程），-ivh选项用于指定以进度条的形式显示将安装过程
rpm -ivh /root/vsftpd-3.0.3-34.el8.x86_64.rpm

```

### rpm

```
RPM全称是Red Hat Package Manager（Red Hat包管理器）。几乎所有的Linux发行版本都使用这种形式的软件包管理安装、更新和卸载软件。rpm有五种基本的操作功能：安装、卸载、升级、查询和验证。

rpm -ivh   包名  直接安装软件包
rpm -evh  软件名  卸载软件包
rpm -qa    查看系统所有已安装的软件包
rpm -ql     查询rpm包中的文件安装的位置
rpm -qf     查看某个文件是由哪个包释放的

```

### yum

```
YUM 是一个在Fedora和RedHat以及SUSE中的Shell前端软件包管理器。yum的宗旨是自动化地升级，安装/移除rpm包，收集rpm包的相关信息，检查依赖性并自动提示用户解决。

主配置文件： /etc/yum.conf

子配置文件：/etc/yum.repos.d/*.repo

yum仓库配置
       [BaseOS]
       name=BaseOS （此条不重要，可忽略但一般会写上）
       baseurl=file:///mnt/BaseOS
       gpgcheck=0    (1 指公司开启要的一个验证，0 表示关闭验证)

1) yum install 安装；

2) yum remove卸载；

3) yum update 升级制定软件

yum和rpm区别

共同点都是可以对rmp包做一个处理。
rpm缺点：如果软件出现依赖关系，不会动态处理，只能手动指定多个包同时安装。
yum 可以自动处理依赖关系，也会把依赖所需要的包全部做一个反向指定处理，用户不需要指定。

```

```
yum -y install httpd

卸载旧版本的 Docker
列出系统中已安装的docker包：
yum list installed | grep docker
卸载已安装的docker包：
yum -y remove docker-ce-cli.x86_64
yum -y remove docker-ce.x86_64
yum -y remove containerd.io
如果系统中没有 Docker，则直接进入下一步。
安装相关依赖
安装 Docker 所需的依赖：
yum install -y yum-utils device-mapper-persistent-data lvm2
添加 Docker 的 yum 源：
yum-config-manager --add-repo https://mirrors.cloud.tencent.com/docker-ce/linux/centos/docker-ce.repo
安装最新版的 Docker
yum 安装 Docker：
yum install -y docker-ce docker-ce-cli containerd.io
验证 Docker 版本以确认安装成功：
docker version
如图所示，Docker 安装成功：

启动 Docker
执行以下命令启动 Docker：
systemctl start docker
然后将 Docker 设置为开机启动：
systemctl enable docker
查看 Docker 运行状态：
service docker status
配置镜像加速
创建 Docker 配置目录：
mkdir -p /etc/docker
配置 Docker 镜像加速源：
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://mirror.ccs.tencentyun.com"]
}
EOF
重启守护进程并重启 Docker：
systemctl daemon-reload && systemctl restart docker
重启完成后，镜像加速即配置成功。
运行第一个容器
使用 docker run 命令可以直接拉取镜像并运行一个容器，例如：
docker run --name=hello hello-world
这行命令会直接拉取 hello-world 镜像，然后运行一个 hello 容器，可以通过以下命令查看该容器的进程：
docker ps -a
可以看到 hello 容器已经运行过了：
拉取镜像
我们也可以一步一步来运行容器。以 calibre-web 为例，先拉取 Docker 镜像：
docker pull johngong/calibre-web
查看现有的镜像：
docker images
如图所示，calibre-web 镜像拉取成功：
创建容器
镜像拉取成功后，根据镜像创建容器：
docker create --name=calibre-web -p 80:8083 -v /data/calibre-web/library:/library -e WEBLANGUAGE=zh_CN johngong/calibre-web
其中：
docker create 是创建容器的命令
--name=calibre-web 表示创建的容器的名称
-p 80:8083 表示该容器将 80 端口映射到 8083 端口
-v /data/calibre-web/librery:/libray 表示该容器将 /data/calibre-web/library 目录映射为 /library 目录
-e WEBLANGUAGE=zh_CN 表示该容器定义了一个变量，变量名是 WEBLANGUAGE，变量值是 zh_CN
johngong/calibre-web 是容器的镜像，这里也就是我们前面拉取的镜像
#### 查看容器

使用如下命令可以查看现有的全部容器：

```

docker ps -a

如图所示，calibre-web 容器创建成功：

![https://academy-lab-prd-pub-1258344699.cos.ap-guangzhou.myqcloud.com/lab-prd/contribution-attachment/100021000426/1638710918507-4.png](https://academy-lab-prd-pub-1258344699.cos.ap-guangzhou.myqcloud.com/lab-prd/contribution-attachment/100021000426/1638710918507-4.png)

image

与 docker run 不同的是，docker create 创建出来的容器不会直接运行。可以查看下运行中的容器进程：

```
docker ps
```

可以看到，没有任何容器在运行：

![https://academy-lab-prd-pub-1258344699.cos.ap-guangzhou.myqcloud.com/lab-prd/contribution-attachment/100021000426/1638710927463-5.png](https://academy-lab-prd-pub-1258344699.cos.ap-guangzhou.myqcloud.com/lab-prd/contribution-attachment/100021000426/1638710927463-5.png)

#### 启动容器

使用以下命令启动刚才创建好的容器：

```
docker start calibre-web
```

查看容器进程：

docker ps

可以看到，calibre-web 容器正在运行：

![https://academy-lab-prd-pub-1258344699.cos.ap-guangzhou.myqcloud.com/lab-prd/contribution-attachment/100021000426/1638710948194-6.png](https://academy-lab-prd-pub-1258344699.cos.ap-guangzhou.myqcloud.com/lab-prd/contribution-attachment/100021000426/1638710948194-6.png)

#### 停止容器

要停止正在运行的容器有两种方法。一种是 docker stop，例如：

```
docker stop calibre-web
```

使用 docker ps 命令可以看到，正在运行的容器中已经没有 calibre-web 了：

![https://academy-lab-prd-pub-1258344699.cos.ap-guangzhou.myqcloud.com/lab-prd/contribution-attachment/100021000426/1638710990113-7.png](https://academy-lab-prd-pub-1258344699.cos.ap-guangzhou.myqcloud.com/lab-prd/contribution-attachment/100021000426/1638710990113-7.png)

image

另一种方法是 docker kill，例如：

```
docker kill calibre-web
```

这两种方法的区别在于，docker stop 会给时间让容器保存最后的运行状态，而 docker kill 则会直接关闭容器。 #### 删除终止状态的容器

使用 docker rm 命令可以删除指定的容器，例如：

```
docker rm hello
```

查看所有容器：

```
docker ps -a
```

已经看不到 hello 容器了：

![https://academy-lab-prd-pub-1258344699.cos.ap-guangzhou.myqcloud.com/lab-prd/contribution-attachment/100021000426/1638711034233-8.png](https://academy-lab-prd-pub-1258344699.cos.ap-guangzhou.myqcloud.com/lab-prd/contribution-attachment/100021000426/1638711034233-8.png)

删除运行状态的容器 我们先重新运行 calibre-web 容器： docker start calibre-web 这时候我们用 docker rm 删除该容器： docker rm calibre-web 命令行会报错： image 要删除运行状态的容器，需要带上 -f 选项： docker rm -f calibre-web 正在运行的 calibre-web 会被强制停止并删除。 删除指定镜像 使用 docker rmi 命令可以删除指定的镜像，例如： docker rmi hello-world 查看现有镜像： docker images 已经看不到 hello-world 镜像了： image 删除所有镜像 我们可以通过 docker rmi 跟镜像 ID 来删除指定的镜像。而获取所有镜像 ID 的命令是： docker images -q 如图所示，命令行列出了剩余所有镜像的 ID： image 我们可以用这些 ID 一次性删除所有镜像： docker rmi

```
docker images -q
```

现在用 docker images 已经看不到镜像了：

```
### mongodb
### 下载启动 MongoDB

Leanote 依赖 MongoDB 作为数据存储，下面开始安装 MongoDB：

#### 下载 MongoDB

进入 [/home](javascript:void(0);) 目录，并下载 MongoDB：

```

cd /home

```

下载源码：

```

wget http://labs-1253675457.cosgz.myqcloud.com/mongodb-linux-x86_64-3.0.1.tgz

```

解压缩源码包：

```

tar -xzvf mongodb-linux-x86_64-3.0.1.tgz

```

#### 创建用于存储的文件夹目录

```

mkdir -p /data/db

```

#### 配置 MongoDB 的环境变量

编辑 [/etc/profile](javascript:void(0);)，在文件末尾追加以下配置：

profile

```

export PATH=$PATH:/home/mongodb-linux-x86_64-3.0.1/bin

```

并执行以下命令，使环境变量生效。

```

source /etc/profile

```

#### 启动 MongoDB

```

mongod –bind_ip localhost –port 27017 –dbpath /data/db/ –logpath=/var/log/mongod.log –fork

```

**注意**：启动可能需要 3 ~ 5 分钟，耐心等待。

### 安装 Leanote

下面开始安装 Leanote

#### 下载 Leanote

先进入 [/home](javascript:void(0);) 目录

```

cd /home

```

下载 Leanote 源码

```

wget http://labs-1253675457.cosgz.myqcloud.com/leanote-linux-amd64-v2.4.bin.tar.gz

```

解开压缩包：

```

tar -zxvf leanote-linux-amd64-v2.4.bin.tar.gz

```
#### 编辑 Leanote 配置文件

编辑文件 [/home/leanote/conf/app.conf](javascript:void(0);)，在文件中找到 `app.secret=` 项，并修改为如下内容：

```

app.secret=qcloud666

```
#### 初始化数据库

导入初始化数据：

```

mongorestore -h localhost -d leanote –dir /home/leanote/mongodb_backup/leanote_install_data/

```
#### 启动 Leanote 服务

```

nohup /bin/bash /home/leanote/bin/run.sh >> /var/log/leanote.log 2>&1 &

```
#### 通过 ip 访问笔记本

通过访问 [http://43.138.152.254:9000](http://43.138.152.254:9000 "null") 就可以了使用自己的笔记本。

*   初始化账户：

```

admin

```

*   初始化密码：

```

abc123

请务必修改密码已确保使用安全！

### linux端口占用

lsof -i:端口号 kill -9 PID

### 宝塔

其实没有域名也是可以用ip地址，搭建网站的，在宝塔面板部署网站的时候，填上ip地址就行。

如果想要搭建多个网站，可以在后面加上端口号

![https://img-blog.csdnimg.cn/20200701212435771.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3l6eno2Ng==,size_16,color_FFFFFF,t_70](https://img-blog.csdnimg.cn/20200701212435771.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3l6eno2Ng==,size_16,color_FFFFFF,t_70)

## 后台开源服务总结

[网盘管理工具](https://github.com/alist-org/alist)

## 文件恢复工具

extundelete

### nginx教程博客

[https://github.com/jaywcjlove/nginx-tutorial](https://github.com/jaywcjlove/nginx-tutorial)


### tcpdump使用
`tcpdump -i eno2 -w temp.pcap` 指定网口eno2
### https证书
`openssl req -x509 -newkey rsa:4096 -sha256 -nodes -keyout privkey.pem -out cacert.pem -days 3650
` 生成key.pem和cert.pem
