---
layout: pages
title: cookie、LocalStorage、sessionStorage三者区别以及使用方式
date: 2020-03-31 17:28:20
categories: "js"
tags: ["html5","js"]
---

# 基本概念
##  Cookie
cookie用来保存客户浏览器请求服务器页面的请求信息。

##  localStorage
本地存储
##  sessionStorage
会话存储

# 区别

## 生命周期

cookie：可以通过expires设置失效时间，不设置默认关闭浏览器即失效

localStorage：除非手动清除，否则永久保存

sessionStorage：仅在当前会话时候生效，关闭页面即失效

## 存储大小

cookie:4KB左右

localStorage、sessionStorage:可以保存5M的信息

## HTTP请求

cookie:每次都会携带在http头中，过多使用cookie会带来性能问题

localStorage、sessionStorage:仅在客户端（即浏览器）中保存，不参与和服务器的通信

## 易用性

cookie:需要程序员自己封装，源生的Cookie接口不友好

localStorage、sessionStorage：源生接口可以接受，亦可再次封装来对Object和Array有更好的支持

## 应用场景

cookie：适合识别用户登录

localStorage和sessionStorage唯一的差别一个是永久保存在浏览器里面，一个是关闭网页就清除了信息

localStorage：可以用来跨页面传递参数（跨tab,多个浏览器窗口）

sessionStorage：用来保存临时数据，防止用户刷新页面之后丢失参数（当前浏览器tab,切换tab无效）

## 使用方式

localStorage和sessionStorage所使用的方法是一样的

设置本地存储
```js
localStorage.setItem('user','小明');
sessionStorage.setItem('user','小明');
```

获取本地存储
```js
localStorage.getItem('user');
sessionStorage.getItem('user');
```

删除本地存储
```js
localStorage.removeItem('user');
sessionStorage.removeItem('user');
```

清除本地存储
```js
localStorage.clear();
sessionStorage.clear();
```

设置cookie
```js
document.cookie = 'name'+username
```

获取cookie
```js
document.cookie
```
