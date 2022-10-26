---
layout: post
title: express+ejs实现前端打包后项目线上运行
categories: [express,vue3,webpack]
description: 通过express+ejs运行打包后的静态资源，搭建一个前端上线项目
keywords: express,ejs
---

## 项目背景

最近在研究vue3项目的打包优化，分割代码体积来实现性能优化，然后打包后想模拟线上运行模式打开项目，所以就用express+ejs实现打包后代码运行观测

[github项目地址](https://github.com/sskun/vue3-imitate-h5)

## 代码明细

此项目就是在VUE3项目基础上进行处理的
ejs和express 使用方法自行百度，本文记录功能代码

### server.js

> 开启80端接口服务

```javascript
const express = require('express')
const app = express()
const path = require('path')

app.set('views', __dirname + '/' + 'dist') // 定义ejs view
app.set('view engine', 'ejs')

app.use('/js/', express.static(path.resolve(__dirname, 'dist/js'))) // js 目录
app.use('/css/', express.static(path.resolve(__dirname, 'dist/css'))) // css 目录

app.get('/*', function (req, res) {
  // 读取ares的一些逻辑这里处理
  res.render('index', {})
})

app.listen(80, () => {
  console.log('服务已启动，80端口监听中...')
})

```

### copyejs.js

> 其实就是把打包后的html复制一个ejs文件出来

```javascript
const path = require('path')
const fs = require('fs')
const fromFileName = path.resolve(__dirname, './dist/index.html')
const toFileName = path.resolve(__dirname, './dist/index.ejs')
fs.copyFile(fromFileName, toFileName, 0, () => {
  console.log('复制完成')
})

```

最后更改指令，在打包成功后运行copyejs，复制文件

```
"build": "vue-cli-service build && node copyejs.js"
```

