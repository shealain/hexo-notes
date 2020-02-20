---
title: node如何通过express构建一个服务
date: 2020-02-18 20:20:02
categories: "express"
tags: ["JavaScript", "node","express"]
---


# 创建并初始化项目 

创建一个目录并进入此目录并将其作为当前工作目录
~~~ JavaScript
    mkdir myapp
    cd myapp
~~~

通过 npm init 命令为你的应用创建一个 package.json 文件
~~~ JavaScript
    npm init
~~~

# 构建一个服务
新建一个文件server.js
~~~ JavaScript
    const express = require('express')
    const app = express()
    app.listen(3000, () => console.log('服务启动成功，请访问localhost:3000'))
~~~
# 利用 Express 托管静态文件 
基本用法：`express.static(root, [options])`

如果要把publish目录暴露出去
~~~js
app.use(express.static('public'))
~~~

暴露当前文件目录
~~~js
app.use(express.static(__dirname))
~~~

# 启动服务
~~~ javascript
    node server.js
~~~

# 路由使用

## 基本用法：`app.METHOD(PATH, HANDLER)`

get:
~~~javascript
app.get('/', function (req, res) {
    res.send('Hello World!')
})
~~~

post:
~~~javascript
app.post('/', function (req, res) {
    res.send('Hello World!')
})
~~~

all:即不同请求方式共用一个方法
~~~javascript
app.all('/', function (req, res) {
    res.send('Hello World!')
})
~~~
其他：option、put、delete、patch等请求方式同理。

## 通过 router 使用路由
~~~javascript
const router = express.Router()
~~~

get:
~~~javascript
router.get('/', function (req, res) {
    res.send('Hello World!')
})
~~~

post:
~~~javascript
router.post('/', function (req, res) {
    res.send('Hello World!')
})
~~~

all:即不同请求方式共用一个方法
~~~javascript
router.all('/', function (req, res) {
    res.send('Hello World!')
})
~~~
其他：option、put、delete、patch等请求方式同理。

使用router添加路由时，需
```javascript
app.use(router)
```

# 捕捉共同错误，设置错误处理器
~~~javascript
app.use(function (err, req, res, next) {
  console.error(err)
  res.status(500).send('Something broke!')
})
~~~

# node利用nodemon插件更新服务时无需重启服务
安装nodemon插件
~~~js
    npm install nodemon -g
~~~
更改启动服务命令
~~~js
    nodemon server.js
~~~

# 了解更多express：
http://www.expressjs.com.cn/en/4x/api.html#req
