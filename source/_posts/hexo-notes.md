---
title: hexo安装及使用
date: 2020-02-18 20:20:02
categories: "hexo"
tags: ["hexo"]
---

# hexo 笔记搭建

## 环境安装

安装 `hexo`

```javascript
npm install hexo -g
```

## 初始化项目

```javascript
hexo init hexo-notes

cd hexo-notes

npm install
```

## 更换 `hexo` 主题

下载主题
```javascript
git clone https://github.com/HeskeyBaozi/hexo-theme-lite themes/lite

```
配置主题

在 `_config.yml` 中找到 `theme` 配置项，将其设置为 `next`：

```javascript
theme: lite
```

## 新建第一个笔记

```javascript
hexo new 'node入门'
```

编辑 `source/_posts/node入门.md`

## 启动本地服务进行预览

```javascript
npm run server
```

## 将源码提交到 `github` 上

在 `github` 上创建一个 `hexo-notes` 的仓库，然后关联

```javascript
git init

git remote add origin https://github.com/shealain/hexo-notes.git
```

提交文件到 `master` 分支

```javascript
git add .

git commit -m 'init project'

git push origin master
```


## 打包

```javascript
npm run build
```

生成的静态文件放置到 `public` 文件夹中

## 部署

准备工作，需要下载关联 `git` 的插件

```javascript
npm install hexo-deployer-git --save
```

修改部署配置，打开 `_config.yml`，找到 `deploy` 配置项

```javascript
deploy:
  type: 'git'
  repo: https://github.com/shealain/shealain.github.io.git
  branch: [master]
```

执行部署命令

```javascript
npm run deploy
```







