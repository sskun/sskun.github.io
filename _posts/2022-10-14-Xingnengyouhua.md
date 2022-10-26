---
layout: post
title: 前端性能优化方案集锦
categories: [性能优化]
description: 本文主要介绍前端性能优化的各种方案,包括打包阶段，缓存阶段，加载资源方式等各种
keywords: Javascript
---

前端性能优化之路漫漫，都是一点一滴的积累起来的，所以也是做一个记录

### 前端性能-gzip压缩

#### 简介
当页面访问我们的web站点的时候，我们的前端资源如果通过GZIP压缩，把压缩后的资源传递客户端可以比纯文件减少大约百分之60左右的体积，可以大大的提高响应速度，节约网络资源。

