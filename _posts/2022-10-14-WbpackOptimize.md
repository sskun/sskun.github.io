---
layout: post
title: 前端性能优化之webpack篇
categories: [前端性能优化,webpack]
description: 本文主要介绍通过webpack优化构建代码，优化打包后的资源实现资源文件体积的优化。
keywords: webpack
---

> 一个页面从输入地址到前端展示有一个很重要的过程就是资源的加载，在这个过程我们前端能做的就是尽可能的优化资源的体积，保证资源加载的速度。这就要求我们对资源进行压缩与合并，这就需要对构建工具webpack进行合理的配置来优化代码打包。

## webpack性能优化之gzip

### 介绍

首先我们对比webpack开启gzip格式打包后的文件和原来的打包文件大小差距还是很大的、

![image](http://kunyk.gitee.io/sansssimg/images/optimize/gzip01.jpg)


> 我们所说的GZIP压缩其实是HTTP压缩里面的一种压缩类型,HTTP 压缩就是以缩小体积为目的，对 HTTP 内容进行重新编码的过程。Gzip 的内核就是 Deflate，目前我们压缩文件用得最多的就是 Gzip。可以说，Gzip 就是 HTTP 压缩的经典例题。


接下来我们来看一张浏览器实际请求示例

![image](http://kunyk.gitee.io/sansssimg/images/optimize/gzip03.jpg)


开启gzip只需要在 request headers  里面加 accept-encoding:gzip 即可开启

然后 reponse header指定Content-Encoding首部，告诉客户端response的压缩格式，这样客户端才能正确解压。

### 使用
 
weback 要配合compression-webpack-plugin 插件使用

[compression-webpack-plugin插件使用方法](https://github.com/webpack-contrib/compression-webpack-plugin)


## webpack性能优化之代码分割打包

### 使用方法

这个主要是 split-chunks-plugin 插件的使用，使用方法参考下面的链接，主要的思路其实就是重复代码合并打包，然后对node_modules里面的包分割处理，

[split-chunks-plugin配置地址](https://webpack.docschina.org/plugins/split-chunks-plugin/)

### 项目配置示例

```javascript
    config.optimization.splitChunks({
      chunks: 'all', // 2. 处理的 chunk 类型
      minSize: 20000, // 4. 允许新拆出 chunk 的最小体积
      minRemainingSize: 0,
      minChunks: 1, // 5. 拆分前被 chunk 公用的最小次数
      maxAsyncRequests: 30, // 7. 每个异步加载模块最多能被拆分的数量
      maxInitialRequests: 30, // 6. 每个入口和它的同步依赖最多能被拆分的数量
      enforceSizeThreshold: 50000, // 8. 强制执行拆分的体积阈值并忽略其他限制
      cacheGroups: {
        defaultVendors: {
          test: /[\\/]node_modules[\\/]/, // 1.1 模块路径/文件名匹配正则
          priority: -10, // 1.2 缓存组权重
          reuseExistingChunk: true // 1.3 复用已被拆出的依赖模块，而不是继续包含在该组一起生成
        },
        'vendors-base': {
          name: 'vendors-base',
          test: /[\\/]node_modules[\\/](vue|vue-router|axios)/, // 打包vue相关的公用模块
          chunks: 'all',
          priority: 10,
          enforce: true
        },
        'vendors-console': {
          name: 'vendors-console',
          test: /[\\/]node_modules[\\/](ant-design-vue|moment)/, // 打包指定的大的三方插件
          chunks: 'all',
          priority: 8,
          enforce: true
        },
        'chunk-vendors': {
          name: 'chunk-vendors',
          test: /[\\/]node_modules[\\/]/, // 打包剩余node_modules插件
          chunks: 'all',
          priority: 1,
          enforce: true
        }
      }
    })
```





