---
layout: pages
title: GitHub如何新建仓库和提交代码
date: 2020-03-31 22:29:54
categories: "js"
tags: ["git","js"]
---

# GitHub中新建仓库
首先进入到自己的主页https://github.com

![Image text](/images/git1.png)

新建一个仓库

![Image text](/images/git2.png)

在输入完上面需要填入的内容后，点击”Create repository”，就创建完成了；

找到当前项目并拷贝路径
![Image text](/images/git3.png)

# 在本地与github项目进行关联

先初始化git项目

```javascript
git init
```

添加远程管理
```javascript
git remote add origin https://github.com/shealain/hexo-notes.git
```

提交文件到github `master` 分支
```javascript
git add .

git commit -m 'init project'

git push origin master
```

把GitHub文件下载下来
```javascript
git add .

git commit -m 'init project'

git push origin master
```