# 快速创建一个最简单的 node 服务

slug: node
status: Published
tags: other
type: Post

1、生成 package.json 文件

```bash
npm init -ynpm install express
```

2、创建并编写 js 文件，例如：server.js

```
var express = require("express"); //导入express框架
var bodyParser = require("body-parser"); //http请求参数解析
var app = express(); //生成实例

//定义接口
app.get("/api/getList", function (request, response) {
  response.send("listData");
});

app.listen(80, function () {
  console.log("Node服务已启动");
});
```

3、在控制台执行命令，启动服务

```scss
node server.js
```

4、浏览器或 PostMan 访问地址， [http://localhost:3000/api/getList](http://localhost:3000/api/getList)