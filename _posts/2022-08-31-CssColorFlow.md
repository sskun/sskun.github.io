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
效果可以参考文章底部地址

### 流动效果

> 实现流动效果的背景色方法很多，比如使用背景图，让图去移动是可以实现的，使用gif图也是可以实现的，这些是需要UI配合出图就可以了，今天主要讲纯CSS实现这个效果

#### 方法一：利用hue-rotate去实现

代码如下，这个方法主要是改变了颜色的色相，效果看起里很流畅，但是因为是改变色相，所以中间流动的颜色我们没办法控制

```css
.flow-colorful {
    max-width: 600px;
    height: 150px;
    background: linear-gradient(to right, red, yellow);
    animation: hue 6s linear infinite;
    text-align: center;
    line-height: 150px;
    color: #fff;
}
@keyframes hue {
    from { filter: hue-rotate(0deg); }
    to { filter: hue-rotate(360deg); }
}
```

#### 方法二：利用放大背景色去实现

代码如下,这个思路就是方法背景，然后利用background-position的位置移动然后形成视觉上移动的效果，
注意这个颜色的位置和比例

```css
.static-colorful03{
    background-image: linear-gradient(to right, #16A085 0%, #F4D03F 51%,  #16A085  100%);
    text-transform: uppercase;
    text-align: center;
    background-size: 200% auto;
    transition: 0.5s;
    animation: colorful03 3s linear infinite;
}
.static-colorful03:hover {
     background-position: right center;
     text-decoration: none;
}
@keyframes colorful03{
    0% {background-position: right}
    50% {background-position: left}
    100% {background-position: right}
}
```

同样也可以利用鼠标移动实现酷炫的效果,原理都是同上

```css
.static-colorful04{
    background-image: linear-gradient(to right, #16A085 0%, #F4D03F 51%,  #16A085  100%);
    text-transform: uppercase;
    text-align: center;
    background-size: 200% auto;
    transition: 0.5s;
}
.static-colorful04:hover {
     background-position: right center;
     text-decoration: none;
}
```

### 总结
之前总是让颜色移动来实现，这种效果很不佳，因为背景色的动画不支持线性变化，所以很是生硬，换个思路看问题，可以让背景去移动。

[上面所有的DEMO地址](https://jsrun.net/pFPKp)

