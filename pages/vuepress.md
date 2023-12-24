# vuepress

slug: vuepress
status: Published
tags: blog
type: Post

## vuepress 使用

[[toc]]

## 简单部署开发

### clone 项目

> git clone -b all-files https://github.com/cvabm/cvabm.github.io.git
> 

### 安装 vuepress

> yarn add -D vuepress # 或者：npm install -D vuepress
> 

### 开发生成预览

> yarn docs:dev # 或者：npm run docs:dev
> 
> 
> 浏览器访问 loalhost:8080
> 
> 单独编译
> 
> yarn docs:build # 或者：npm run docs:build
> 

### 部署发布

> 执行./.deploy.sh 如果没权限，chmod 777 deploy.sh
> 

### picgo 配置 github 图床

> 1：https://github.com/Molunerfinn/PicGo 下载 dmg 文件安装
> 
> 
> 2：github 头像 - setting - developer setting - personal access tokens - regenerate token
> 
> 3：配置 picgo
> 
> 第一行设定仓库名按照“账户名/仓库名的格式填写”，比如我的是：flighty/img
> 
> 第二行分支名统一填写“master”
> 
> 第三行将之前的 Token 粘贴在这里
> 
> 第四行留空
> 
> 第五行自定义域名的作用是在上传图片后成功后，PicGo 会将“自定义域名+上传的图片名”生成
> 
> 的访问链接，放到剪切板上，自定义域名需要按照这样去填写：
> 
> https://raw.githubusercontent.com/账户名/仓库名/master，
> 
> 比如我的是：https://raw.githubusercontent.com/flighty/images/master
> 

参考：[https://blog.csdn.net/qq_43750573/article/details/104522323](https://blog.csdn.net/qq_43750573/article/details/104522323)

## 全局搜索

[https://learnku.com/articles/12400/using-algolia-docsearch-to-easily-realize-document-total-station-search](https://learnku.com/articles/12400/using-algolia-docsearch-to-easily-realize-document-total-station-search)

## 继承主题(修改样式、布局)

```
1：在docs路径下执行 vuepress eject
2: 在以下路径文件顶部插入以下代码
// docs/.vuepress/theme/index.js
module.exports = {
  extend: '@vuepress/theme-default'
}

**例子：修改代码字体颜色**
找到以下路径文件
//docs/.vuepress/theme/style/code.styl
修改大约24行处 color #000 ，即可将白色字体改为黑色

```

## netlify

为静态网站提供托管和 serverless 后端服务，与 GitHub 相比，Netlify 托管的网站速度更快，也更稳定

[https://www.netlify.com/](https://www.netlify.com/)

访问地址例：

[https://cvabm.netlify.app/](https://cvabm.netlify.app/)

## cdn 加速

### cloudflare(国外最好免费 CDN)

使用介绍

[https://zhuanlan.zhihu.com/p/82909515](https://zhuanlan.zhihu.com/p/82909515)