---
layout: post
title: Javascript 实现在给定区域随机生成圆形
categories: [Javascript, Html]
description: Javascript, Html
keywords: 前端博客, Javascript, Html
---

以前开发过一个npm包，是一个h5唤醒app的功能，最近优化代码顺便记录下如何开发一个npm包和如何维护包。

### 创建项目

1. npm init 项目 ，生成package.json文件
2. 简单的配置package.json，如下

```javascript
{
  "name": "h5wakeupapp", // 对外是的包名
  "version": "1.0.5", // 最新的版本
  "description": "h5页面唤醒app", // 描述
  "main": "./dist/main.js", // 入口文件
  "files":[], // 白名单
  "scripts": {
    "build": "webpack --mode=production"  // 插件打包
  },
  "author": "sansss", 
  "license": "ISC", //开源协议
  "repository": {
    "type": "git",  // 配置github地址
    "url": "https://github.com/sskun/h5wakeupapp"
  },
  "devDependencies": {
    "babel-core": "^6.26.3",
    "babel-loader": "^7.1.4",
    "babel-polyfill": "^6.26.0",
    "babel-preset-env": "^1.7.0",
    "babel-preset-stage-3": "^6.24.1",
    "webpack": "^5.3.0",
    "webpack-cli": "^4.1.0"
  },
  "peerDependencies": {}
}
```

### 注册npm账号

1. 方法一：[npm网站账号注册地址](https://www.npmjs.com/) 官网注册
2. 方法而：通过终端运行 npm adduser

### npm发布流程

1. 如果终端未登录，则先 npm login ,登陆后的跳过
2. 终端运行 npm  publish 发布


### 注意点

1. 是npm镜像，否则可能报错
```
    npm config set registry https://registry.npmjs.org/
```
2. publish之前压力确认是否登陆
