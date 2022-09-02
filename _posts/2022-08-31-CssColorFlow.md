---
layout: post
title: CSS-颜色的流动与色调变化
categories: [Css]
description:  CSS颜色的流动与色调变化
keywords: Css,颜色的流动,色调
---

利用CSS实现背景色或者字体颜色的渐变和流动效果，linear-gradient属性和CSS内置函数hue-rotate使用记录

### 前言
最近工作上需要实现按钮背景渐变效果，效果是静态的渐变和流动的渐变，下面就简单的说下实现的过程

### 静态的渐变

语法如下，[参考MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/gradient/linear-gradient)

```css
.grad {
  background-color: #F07575; /* 不支持渐变的浏览器回退方案 */
  background-image: -webkit-linear-gradient(top, hsl(0, 80%, 70%), #bada55); /* 支持 Chrome 25 and Safari 6, iOS 6.1, Android 4.3 */
  background-image: -moz-linear-gradient(top, hsl(0, 80%, 70%), #bada55); /* 支持 Firefox (3.6 to 15) */
  background-image: -o-linear-gradient(top, hsl(0, 80%, 70%), #bada55); /* 支持旧 Opera (11.1 to 12.0) */
  background-image: linear-gradient(to bottom, hsl(0, 80%, 70%), #bada55); /* 标准语法; 需要最新版本 */
}
```


也支持下面这种写法,表示left top 是起始色，bottom right 是结束色，中间部分是渐变色

```css
 .grad{
    background-image: linear-gradient(to bottom right, hsl(0, 80%, 70%), #bada55); 
  }
```
效果可以参考下面的地址

[效果地址](https://jsrun.net/pFPKp)

### 流动效果

