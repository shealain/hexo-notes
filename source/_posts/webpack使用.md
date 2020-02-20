---
layout: pages
title: webpack使用
date: 2020-02-20 16:18:18
categories: "webpack"
tags: ["JavaScript", "webpack"]
---

# 概念
本质上，webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。

# 基本元素
入口(entry),输出(output),loader,插件(plugins)

# 入口

单个入口
~~~js
const config = {
  entry: './main.js'
};
module.exports = config;
~~~
单个入口或多个入口
~~~js
const config = {
  entry: {
    main: './main.js',
    app:'./app.js'
  }
};
module.exports = config;
~~~
# 输出
输出单个文件
~~~js
const config = {
  output: {
    filename: 'bundle.js',
    path: './dist'
  }
};
module.exports = config;
~~~
输出多个文件，则使用[`name/hash`]占位符来命名
~~~js
{
  entry: {
    app: './app.js',
    search: './main.js'
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/dist'
  }
}
~~~

# 模式
~~~js
module.exports = {
  mode: 'production', /* development=开发环境，production=生产环境*/
};
~~~
# loader
webpack打包时通过loader用于对模块的源代码进行转换，在使用前通过npm安装。
一般有有三种使用 ~loader~ 的方式：
1.配置：在 webpack.config.js 文件中指定 loader。
~~~js
module.exports = {
  module: {
    rules: [
      { test: /\.css$/, use: 'css-loader' },
      { test: /\.ts$/, use: 'ts-loader' },
      { test: /\.less$/, use: ['style-loader','css-loader']},
    ]
  }
};
~~~~
2.内联：在每个 import 语句中显式指定 loader。
~~~js
import Styles from 'style-loader!css-loader?modules!./styles.css';
~~~
3.CLI：在 shell 命令中指定它们。
~~~js
webpack --module-bind jade-loader --module-bind 'css=style-loader!css-loader'
~~~
