# hexo-notes
my hexo-notes


## 源码位置

```js
https://github.com/shealain/hexo-notes.git
```

运行命令
```js
git add .

git commit -m '注释'

git push origin master
```


## 部署位置

```js
deploy:
  type: 'git'
  repo: https://github.com/shealain/shealain.github.io.git
  branch: [master]
```

运行部署命令

```js
npm run build
npm run deploy
```
