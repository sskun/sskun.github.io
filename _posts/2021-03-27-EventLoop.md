---
layout: post
title: Javascript语言特点的理解和事件循环机制记录
categories: [Javascript]
description: Javascript, EventLoop
keywords: Javascript, EventLoop
---

## JS 语言介绍

> Javascript 一种基于对象(object-based)和事件驱动(EventDriven)的简单的并具有安全性能的脚本语言。
> 特点：解释型、基于对象、事件驱动、跨平台。弱类型

#### 解释型语言

> 对程序来说，计算机需要一个"翻译"，即把程序代码变成计算机可以理解的语言：0 和 1 组成的包含信息的序列。目前存在两种翻译类型：一个是编译，一个是解释。两种方式都需要对代码进行翻译，只是翻译的时间不同而已。

> 编译型语言在计算机运行代码前，先把代码翻译成计算机可以理解的文件

> 解释型语言则不同，解释型语言的程序不需要在运行前编译，在运行程序的时候才翻译，专门的解释器负责在每个语句执行的时候解释程序代码

所以 js 只有在执行的时候知道我们语法上的错误

#### 单线程

##### 一、为什么是单线程

因为在设计之初，js 是浏览器脚本语言，主要工作是浏览器和使用者之间的交互以及操作 dom，这就决定只能是单线程，同一时间只能执行一个任务。

为了利用多核 CPU 的计算能力，HTML5 提出 Web Worker 标准，允许 JavaScript 脚本创建多个线程，但是子线程完
全受主线程控制，且不得操作 DOM。所以，这个新标准并没有改变 JavaScript 单线程的本质。

---

## 事件循环机制（Event loop）

> 在说这个之前我们要先了解 js

#### 为什么设计事件循环机制

因为 js 语言是单线程的执行机制，所以所有的任务都要排队执行，上一个任务执行完毕才会执行下一个任务，在我们的实际开发场景中，有许多时间久的 i/o 任务，这样必须要慢慢的等这个任务执行完毕，在进行下一个，js 语言设计者就考虑这时候完全可以不管 i/o 设备。先把他挂起，去执行后面的任务，等 io 设备输出结果，再把他拿回来去执行，这样的思想就形成了我们的时间循环机制。

#### 关键名词理解

异步：是关于现在和将来的时间间隙，异步任务是相对于当前任务经过一些时间后执行的任务

并发：是关于能够同时发生的事情，并行的任务可以同时执行。

事件循环：主线程从任务队列中读取和执行事件的过程，且不断循环

#### 事件循环机制规则

- 主线程任务执行
- 遇到异步任务，放到异步队列
- 区分异步任务是微任务还是宏任务
- 同步任务执行完毕，执行微队列任务，先进先出的原则
- 微队列任务执行完毕执行宏队列任务

```javascript
setTimeout(function () {
  console.log('1')
})

new Promise(function (resolve) {
  console.log('2')

  for (var i = 0; i < 1000; i++) {
    i == 99 && resolve()
  }

  console.log('3')
}).then(function () {
  console.log('4')
})

console.log('5')

// 执行结果  2 3 5 4 1
```

#### 任务明细

1. 宏任务：1. script (可以理解为外层同步代码)、setTimeout/setInterval、UI rendering/UI 事件、postMessage、MessageChannel、setImmediate，I/O（Node.js）
2. 微任务：async/await、promise、

## Web Workers
