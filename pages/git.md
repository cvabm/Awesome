# git

slug: git
status: Published
tags: 开发工具
type: Post

# git

简单易学[https://learngitbranching.js.org/](https://learngitbranching.js.org/)

命令行提示[https://fig.io](https://fig.io/) [https://gitsheet.wtf/](https://gitsheet.wtf/) [https://www.progit.cn/](https://www.progit.cn/)

[https://github.com/k88hudson/git-flight-rules/blob/master/README_zh-CN.md](https://github.com/k88hudson/git-flight-rules/blob/master/README_zh-CN.md)

[[toc]]

## 常见问题

> idea push reject：push mater to origin/master was rejected by remote
> 
> 
> 没权限
> 

# 提交历史

git log git log –online :精简模式

## 常用 git 命令

```
git add . //
git commit -s
git commit --amend //在原记录上提交
git status  查看修改后的代码
git branch -a 查看远程分支
git branch   查看本地分支
git rm 删除
git rm -rf 强制删除
git diff 后跟文件路径 ---//查看修改的地方
git branch -D分支名  删除分支
gitk .  查看修改记录

repo upload上传
repo sync . 更新代码
repo start tag .   /空格+点  在所在目录新建分支

adb reboot  ---重启

```

## commit 后撤销

```
git reset --soft HEAD^

仅仅是撤回commit操作，您写的代码仍然保留。
HEAD^的意思是上一个版本，也可以写成HEAD~1

如果你进行了2次commit，想都撤回，可以使用HEAD~2
--mixed
意思是：不删除工作空间改动代码，撤销commit，并且撤销git add . 操作
这个为默认参数,git reset --mixed HEAD^ 和 git reset HEAD^ 效果是一样的。

--soft
不删除工作空间改动代码，撤销commit，不撤销git add .

--hard
删除工作空间改动代码，撤销commit，撤销git add .

注意完成这个操作后，就恢复到了上一次的commit状态。

顺便说一下，如果commit注释写错了，只是想改一下注释，只需要：
git commit --amend

此时会进入默认vim编辑器，修改注释完毕后保存就好了。
————————————————
版权声明：本文为CSDN博主「天空还是那么蓝」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/w958796636/java/article/details/53611133

```

## git 删除本地未提交的文件

```
git checkout .

git clean -xdf
```

## 提取 git 某条提交记录中更改的文件

```
windows：
git archive -o upadate.zip HEAD $(git diff-tree -r --no-commit-id --name-only --diff-filter=ACMRT <comit_id>)

linux:
git log f3794bd30cb1d3f8e64f1177d3149f28cbc828e6 -1 --name-only | grep '/' | awk '{print $1}' > list.txt
# 在当前目录下，创建temp目录
mkdir temp
# 将已修改文件列表逐一复制到当前目录下的temp目录
xargs -a ./list.txt cp --parents -t ./temp

# 将temp目录下的所有文件打包为modules.tar.gz
cd temp
tar -czf modules.tar.gz *
```

## 提取 git 尚未提交的更改文件

```
# 在源代码根目录，使用git status命令获取已修改文件的列表
git status | grep modified | awk '{print $2}' > list.txt
# 在当前目录下，创建temp目录
mkdir temp
# 将已修改文件列表逐一复制到当前目录下的temp目录
xargs -a ./list.txt cp --parents -t ./temp

# 将temp目录下的所有文件打包为modules.tar.gz
cd temp
tar -czf modules.tar.gz *
```

## git 设置和取消代理
- 注意端口是否正确，不一定是1080：clash  -general - port

设置 git 代理
git config –-global http.proxy http://127.0.0.1:1080
git config –-global https.proxy https://127.0.0.1:1080  

检查设置是否成功：
git config --global --get http.proxy
git config --global --get https.proxy

去掉 git 代理
git config -–global –-unset http.proxy
git config –-global –-unset https.proxy

## git 配置用户名邮箱

```
修改当前项目的用户名和邮箱地址：

$ git config  user.name  "username"

$ git config  user.email  "email"
修改全局用户名和邮箱地址：

$ git config --global user.name "username"

$ git config --global user.email "email"
查看git用户名和邮箱地址命令：

$ git config user.name

$ git config user.email
```

## git 配置秘钥

- 生成秘钥

```
ssh-keygen -t rsa -C "youremail@example.com"

命令要求输入密码，这个时候不用输入，直接三个回车即可。
这条命令的目的是为了让本地机器ssh登录远程机器上的GitHub账户无需输入密码。
```

- 将 SSH key 添加到 ssh-agent`ssh-add C:/Users/Administrator/.ssh/id_rsa`
- 将 SSH key 添加到你的 GitHub 账户
在账户选项中选择 “Settings”–>“SSH and GPG keys”–>“New SSH key”，然后打开之前新生成的 id_rsa.pub 文件，将密钥复制后填写到账户中【注意填写时的格式要求】

---

问题一

Windows 下使用 ssh-add 报错 Error connecting to agent: No such file or directory

终端:Windows PowerShell

- 检查 ssh-agent 服务是否启动成功

```powershell
PS D:\code> get-service ssh*Status   Name               DisplayName------   ----               -----------Stopped  ssh-agent          OpenSSH Authentication Agent
```

- 发现 ssh-agent 服务状态为 stopped,启动服务

```powershell
PS D:\code> Set-Service -Name ssh-agent -StartupType ManualPS D:\code> Start-Service ssh-agent
```

- 执行 ssh-add 命令检查是否成功

```powershell
PS D:\code> ssh-add -l2048 SHA256:Dw8iD5trSzInnsmmDpaXBusdfL2K3wM3b+GMulKNHbAU C:\Users\Administrator\.ssh\xxx-pc (RSA)2048 SHA256:Mb4qKSueS8bqNALm3423eD98KdTIuEwnLvfVWTNPCusg C:\Users\Administrator\.ssh\yyy (RSA)2048 SHA256:nyLi89QHTYFMr97sM0cG9I6sBfA82GpR9Os2WF0HlwA C:\Users\Administrator\.ssh\id_rsa (RSA)
```

- 问题解决

## git fetch

git pull origin master //相当于进行了 git fetch 和 git merge 两部操作

## git -b 指定分支

```

git clone -b v2.8.1 https://git.oschina.net/oschina/android-app.git

```

## git tag 指定 tag

git clone –branch tag 名称 地址

## git tag 历史排序

git tag -n –sort=taggerdate

更多 log：git log –pretty=oneline

## 只 clone 最新的一个版本记录

git clone address –depth=1

## github 下载指定文件夹

[https://minhaskamal.github.io/DownGit/#/home](https://minhaskamal.github.io/DownGit/#/home)

[http://kinolien.github.io/gitzip](http://kinolien.github.io/gitzip)

[http://blog.luckly-mjw.cn/tool-show/github-directory-downloader/index.html](http://blog.luckly-mjw.cn/tool-show/github-directory-downloader/index.html)

## github actions

打印当前文件夹下所有文件夹和文件名（包括子文件夹）

```
        echo "Current Path: $PWD"
        echo "Directories:"
        find . -type d -print
        find . -type d
        echo "Files:"
        find . -type f -print
```

### 编译 apk 并发布 Release

```
name: Build and Release

on:
  push:
    branches:
      - master
      - "feature/*"
    tags:
      - "v*.*.*"
  pull_request:
    branches:
      - master
      - "feature/*"

jobs:
  apk:
    name: Generate APK
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v1
      - name: set up JDK 1.8
        uses: actions/setup-java@v1
        with:
          java-version: 1.8
      - name: set up JDK 1.8
        uses: gradle/gradle-build-action@v2
        with:
          gradle-version: 6.1.1
      - name: Build with Gradle
        run: gradle assembleRelease
      - name: Upload APK
        uses: actions/upload-artifact@v1
        with:
          name: apk
          path: app/build/outputs/apk/release/app-release-unsigned.apk

  release:
    name: Release APK
    needs: apk
    runs-on: ubuntu-latest
    steps:
      - name: Get branch name
        id: branch-name
        uses: tj-actions/branch-names@v5.1
      - name: Print branch
        run: |
          echo "Running on default: ${{ steps.branch-name.outputs.current_branch }}"

      - name: Download APK from build
        uses: actions/download-artifact@v1
        with:
          name: apk
      - name: Create Release
        id: create_release
        uses: actions/create-release@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          tag_name: ${{ github.run_number }}
          release_name: ${{ github.event.repository.name }}  ${{ steps.branch-name.outputs.current_branch }} v${{ github.run_number }}.${{ github.run_attempt }}
      - name: Upload Release APK
        id: upload_release_asset
        uses: actions/upload-release-asset@v1.0.1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          upload_url: ${{ steps.create_release.outputs.upload_url }}
          asset_path: apk/app-release-unsigned.apk
          asset_name: ${{ github.event.repository.name }}  ${{ steps.branch-name.outputs.current_branch }} v${{ github.run_number }}.${{ github.run_attempt }}.apk
          asset_content_type: application/zip

```

### react native 编译 apk

```
jobs:
  apk:
    name: Build mobile bundle (Android)
    runs-on: ubuntu-latest
    steps:
     - uses: actions/checkout@v3
     - uses: actions/setup-node@v3
       with:
         node-version: 16
         cache: 'npm'
     - run: npm install
     - name: Build app
       working-directory: android
       run: ./gradlew assembleRelease -PreactNativeArchitectures=arm64-v8a
#      - run: npx react-native run-android
       continue-on-error: true
     - name: Upload APK
       uses: actions/upload-artifact@v1
       with:
         name: apk
         path: android/app/build/outputs/apk/release/app-release.apk
```

### 语法

```
- run: npm install -g bats

actions/upload-artifact
该操作可以将文件或目录上传为工作流运行的一部分，并指定一个名称用于标识这些上传的产物。
这样，在后续的工作流步骤中，您可以使用 actions/download-artifact 操作来下载这些产物。

runs-on: ubuntu-18.04

continue-on-error: true
忽略报错继续执行下一步

```

**actions/checkout@v1 和 actions/checkout@v3 区别**

1、 v3 支持完整的深层克隆（deep clone），可以获取完整的 Git 历史记录，而 v1 只会获取最近的单个 commit。

2、v1 默认情况下检出代码的是默认分支（通常是 master），而 v3 默认情况下会根据触发工作流的事件自动检出相应的分支或拉取请求。

[https://wangchujiang.com/github-actions/](https://wangchujiang.com/github-actions/)

## fork 项目不可使用 GITHUB_TOKEN 的问题

报错 Resource not accessible by integration

解决：项目- settings -actions - General - Workflow permissions -Read and write

## github 配置 ssh

- 第一步：检查本地主机是否已经存在 ssh key

```bash
cd ~/.sshls//看是否存在 id_rsa 和 id_rsa.pub文件，如果存在，说明已经有SSH Key
```

- 第二步：生成 ssh key

```bash
如果不存在 ssh key，使用如下命令生成ssh-keygen -t rsa -C "xxx@xxx.com"//执行后一直回车即可
```

- 第三步：获取 ssh key 公钥内容（id_rsa.pub）

```bash
cd ~/.sshcat id_rsa.pub复制该内容
```

- 第四步：Github 账号上添加公钥

```
进入 Settings 设置
添加 ssh key，把刚才复制的内容粘贴上去保存即可
```

- 第五步：验证是否设置成功

```bash
ssh -T git@github.com
```

## .gitignore 立即生效

```
# 有时候需要突然修改 .gitignore 文件，随后要立即生效

git rm -r --cached . #清除缓存
git add . #重新trace file
git commit -m "update .gitignore" #提交和注释
git push origin master #可选，如果需要同步到remote上的话
```

## git 重命名文件夹

```
不用先在本地修改文件夹名称
文件夹名称: game   文件夹修改后名称: gamesdk
1.  git mv game gamesdk
2. git commit -m 'rename dir game to gamesdk'
3. 推送到dev 分支
git push origin dev

```

git 在 windows 使用

```
（提交文件到本地分支）
1：新建文件夹 ， cmd进入此目录， git clone ---- （登录gitlab控制台-- 查看http前缀的地址copy）

2：进入到down下来的 项目根目录中 -- git checkout -b  lijiangang   //新建分支
3:  --新建文件android.txt  ，git add 此文件
4： git commit -m "备注"

（本机更新最新的远程变化）
5：git checkout master
6： git pull

（本地合并远程变化）
7： git checkout lijiangang
8：git rebase -i master

（推送本地修修改到远程）
9：git push origin lijiangang

（控制台新建合并请求）
10： 登录gitlab --新建合并请求（输入相关的注释）提交

11：更新本地仓库并删除本地分支
git checkout master
git pull
git branch -d lijiangang

note：git branch --list （查看分支）

```

## gitignore

[https://www.gitignore.io/](https://www.gitignore.io/)

## sourcetree

[https://www.sourcetreeapp.com/](https://www.sourcetreeapp.com/)

## 获取远程仓库地址

`git remote get-url origin`

## 重命名项目

```
git remote -v
git remote rename origin old-origin1
git remote add origin git@123.56.157.156:lijg/XinjiangTongfuvisitor.git
git push -u origin --all
git push -u origin --tags
```

## 关联本地项目到远程库

- **（空仓库）创建完空仓库就将本地项目关联到远程**
1. **如果本地项目已经通过 git 管理：**直接通过 git remote add origin (仓库地址) 关联 => git push -u origin master 推送代码上去，就完事了。
2. **本地项目未通过 git 管理：**git init(将项目通过 git 初始化) => git add .(添加所有修改到暂存区) => git commit -m “first commit remark”(提交 commit) => git remote add origin (仓库地址) => git push -u origin master(推送到远程 github)
- **（非空仓库）创建完非空仓库就将本地项目关联到远程**
1. 远程非空仓库的关联，就要涉及到 2 个不同项目的关联了；得先将远程的代码合并下来，才能提交；我们先假设项目已经通过 git 管理了。缺少关联 push 远程仓库的步骤讲：
2. 关联远程仓库：git remote add origin (仓库地址)
3. git pull origin master –allow-unrelated-histories（意思是 2 个不同项目的没关联提交允许拉取合并）
4. git push origin master（push 成功，完工…）

## git 删除所有 commit 记录

```
删除.git文件夹可能会导致git存储库中的问题。如果要删除所有提交历史记录，但将代码保持在当前状态，可以按照以下方式安全地执行此操作：

git checkout --orphan latest_branch
git add -A
git commit -am "commit message"
git branch -D master
git branch -m master
git push -f origin master
git branch --set-upstream-to=origin/master
```

## git 删除本地分支和远程分支

```
删除远程分支
git branch -a 先查看远程分支

远程：git push origin --delete 分支名
本地：git branch -d 分支名

```

## git 回退

```
git reset HEAD 回退当前版本
git reset HEAD^ 回退上一版本
git reset --hard add或commit后都可以直接回退原始
```

## git 问题：

### remote: Support for password authentication was removed on August 13, 2021

```
重新生成token
setting - developer setting - Personal access tokens - Generate new token
要使用token从命令行访问仓库，请选择repo。
要使用token从命令行删除仓库，请选择delete_repo
其他根据需要进行勾选

git remote set-url origin https://<your_token>@github.com/<USERNAME>/<REPO>.git
<your_token>：换成你自己得到的token
<USERNAME>：是你自己github的用户名
<REPO>：是你的仓库名称

再次push即可
```

## 1、You are about to commit CRLF line separators to the Git repository.

It is recommended to set the core.autocrlf Git attribute to input and and avoid line separator issues.

```
① Git可以在你提交时自动地把行结束符CRLF转换成LF，而在签出代码时把LF转换成CRLF。用`core.autocrlf`来打开此项功能，如果是在Windows系统上，把它设置成`true`，这样当签出代码时，LF会被转换成CRLF：

$ git config --global core.autocrlf true

② Linux或Mac系统使用LF作为行结束符，因此你不想 Git 在签出文件时进行自动的转换；当一个以CRLF为行结束符的文件不小心被引入时你肯定想进行修正，把`core.autocrlf`设置成input来告诉 Git 在提交时把CRLF转换成LF，签出时不转换：

$ git config --global core.autocrlf input

这样会在Windows系统上的签出文件中保留CRLF，会在Mac和Linux系统上，包括仓库中保留LF。

③如果你是Windows程序员，且正在开发仅运行在Windows上的项目，可以设置`false`取消此功能，把回车符记录在库中：

$ git config --global core.autocrlf false
```

## 2、Could not resolve host: gitlab2.xxx.priv

```
1、先切到正常的网络，ping gitlab2.xxx.priv,得到ip:10.200.0.21
2、修改C:\Windows\System32\drivers\etc\HOSTS文件，底部添加：
10.200.0.21 gitlab2.xxx.priv
```

## 删除 tag

```
命令git push origin <tagname>可以推送一个本地标签；

命令git push origin --tags可以推送全部未推送过的本地标签；

命令git tag -d <tagname>可以删除一个本地标签；

命令git push origin :refs/tags/<tagname>可以删除一个远程标签。
```

## shelve changes vs git stash

[https://blog.csdn.net/eclipse1024/article/details/116352777](https://blog.csdn.net/eclipse1024/article/details/116352777)

### 手机端编辑 git 代码

设置秘钥即可推送到远端 github 仓库

官网

[https://spck.io](https://spck.io/)

使用教程

[https://spckio.github.io/spck-documentation/create-app-token.html#](https://spckio.github.io/spck-documentation/create-app-token.html#)

### git 强制推送到远端仓库

```
git init
git add -A
git commit -m 'deploy'
git push -f git@github.com:cvabm/cvabm.github.io.git master
```

### git 本地检出一个新的分支并推送到远程仓库

```
git checkout -b 新分支名
git push --set-upstream origin 分支名
```

### 连接失败报错443问题

dns改为114.114.114.114
### github 加速下载

github.com 改为 github.com.cnpmjs.org 即可

http://tool.mkblog.cn/github/

https://gitclone.com/

https://git.yumenaka.net/

https://gh.con.sh/

https://github.com.cnpmjs.org/

查看git配置信息

git config –global –list

取消设置

git config –global –unset url.https://github.com/.insteadof

raw文件下载加速

原地址：

wget https://raw.githubusercontent.com/kubernetes/kubernetes/master/README.md

替换为

wget https://raw.staticdn.net/kubernetes/kubernetes/master/README.md

提供web界面的github资源加速网站：

GitHub 文件加速：https://gh.api.99988866.xyz/

Github仓库加速：https://github.zhlh6.cn/

Github仓库加速：http://toolwa.com/github/
