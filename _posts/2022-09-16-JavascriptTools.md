---
layout: post
title: JS工具函数助力高效开发
categories: [Javascript]
description: JS工具函数助力高效开发
excerpt: 日常开发中，面对各种不同的需求，我们经常会用到以前开发过的一些工具函数，把这些工具函数收集起来，将大大提高我们的开发效率，本文主要记录并持续更新开发过程中用到的方法...
keywords: Javascript
---

日常开发中，面对各种不同的需求，我们经常会用到以前开发过的一些工具函数，把这些工具函数收集起来，将大大提高我们的开发效率，本文主要记录并持续更新开发过程中用到的方法

### 校验数据类型

> 校验数据类型

```javascript
export const typeOf = function(obj) {
  return Object.prototype.toString.call(obj).slice(8, -1).toLowerCase()
}
typeOf('树哥')  // string
typeOf([])  // array
typeOf(new Date())  // date
typeOf(null) // null
typeOf(true) // boolean
typeOf(() => { }) // function
```

### 防抖函数
```javascript
export const debounce = (() => {
  let timer = null
  return (callback, wait = 800) => {
    timer&&clearTimeout(timer)
    timer = setTimeout(callback, wait)
  }
})()
```

### 节流函数
```javascript
export const throttle = (() => {
  let last = 0
  return (callback, wait = 800) => {
    let now = +new Date()
    if (now - last > wait) {
      callback()
      last = now
    }
  }
})()
```

### 手机号脱敏

```javascript
export const hideMobile = (mobile) => {
  return mobile.replace(/^(\d{3})\d{4}(\d{4})$/, "$1****$2")
}
```

### 开启全屏

```javascript
export const launchFullscreen = (element) => {
  if (element.requestFullscreen) {
    element.requestFullscreen()
  } else if (element.mozRequestFullScreen) {
    element.mozRequestFullScreen()
  } else if (element.msRequestFullscreen) {
    element.msRequestFullscreen()
  } else if (element.webkitRequestFullscreen) {
    element.webkitRequestFullScreen()
  }
}
```

### 关闭全屏

```javascript
export const exitFullscreen = () => {
  if (document.exitFullscreen) {
    document.exitFullscreen()
  } else if (document.msExitFullscreen) {
    document.msExitFullscreen()
  } else if (document.mozCancelFullScreen) {
    document.mozCancelFullScreen()
  } else if (document.webkitExitFullscreen) {
    document.webkitExitFullscreen()
  }
}
```

### 大小写转换

```javascript
// type 1-全大写 2-全小写 3-首字母大写
export const turnCase = (str, type) => {
  switch (type) {
    case 1:
      return str.toUpperCase()
    case 2:
      return str.toLowerCase()
    case 3:
      //return str[0].toUpperCase() + str.substr(1).toLowerCase() // substr 已不推荐使用
      return str[0].toUpperCase() + str.substring(1).toLowerCase()
    default:
      return str
  }
}
```

### 解析url参数

```javascript
export const getSearchParams = () => {
  const searchPar = new URLSearchParams(window.location.search)
  const paramsObj = {}
  for (const [key, value] of searchPar.entries()) {
    paramsObj[key] = value
  }
  return paramsObj
}
```

### 判断手机是Andoird还是IOS

```javascript
/** 
 * 1: ios
 * 2: android
 * 3: 其它
 */
export const getOSType=() => {
  let u = navigator.userAgent, app = navigator.appVersion;
  let isAndroid = u.indexOf('Android') > -1 || u.indexOf('Linux') > -1;
  let isIOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/);
  if (isIOS) {
    return 1;
  }
  if (isAndroid) {
    return 2;
  }
  return 3;
}
```
### 数组对象根据字段去重

```javascript
export const uniqueArrayObject = (arr = [], key = 'id') => {
  if (arr.length === 0) return
  let list = []
  const map = {}
  arr.forEach((item) => {
    if (!map[item[key]]) {
      map[item[key]] = item
    }
  })
  list = Object.values(map)

  return list
}
```
### 滚动到页面顶部

```javascript
export const scrollToTop = () => {
  const height = document.documentElement.scrollTop || document.body.scrollTop;
  if (height > 0) {
    window.requestAnimationFrame(scrollToTop);
    window.scrollTo(0, height - height / 8);
  }
}
```
### 滚动到元素位置

```javascript
export const smoothScroll = element =>{
    document.querySelector(element).scrollIntoView({
        behavior: 'smooth'
    });
};
```
### uuid

```javascript
export const uuid = () => {
  const temp_url = URL.createObjectURL(new Blob())
  const uuid = temp_url.toString()
  URL.revokeObjectURL(temp_url) //释放这个url
  return uuid.substring(uuid.lastIndexOf('/') + 1)
}
```

### 金额格式化

```javascript
// {number} number：要格式化的数字
// {number} decimals：保留几位小数
// {string} dec_point：小数点符号
// {string} thousands_sep：千分位符号
export const moneyFormat = (number, decimals, dec_point, thousands_sep) => {
  number = (number + '').replace(/[^0-9+-Ee.]/g, '')
  const n = !isFinite(+number) ? 0 : +number
  const prec = !isFinite(+decimals) ? 2 : Math.abs(decimals)
  const sep = typeof thousands_sep === 'undefined' ? ',' : thousands_sep
  const dec = typeof dec_point === 'undefined' ? '.' : dec_point
  let s = ''
  const toFixedFix = function(n, prec) {
    const k = Math.pow(10, prec)
    return '' + Math.ceil(n * k) / k
  }
  s = (prec ? toFixedFix(n, prec) : '' + Math.round(n)).split('.')
  const re = /(-?\d+)(\d{3})/
  while (re.test(s[0])) {
    s[0] = s[0].replace(re, '$1' + sep + '$2')
  }

  if ((s[1] || '').length < prec) {
    s[1] = s[1] || ''
    s[1] += new Array(prec - s[1].length + 1).join('0')
  }
  return s.join(dec)
}

```

### 存储操作

```javascript
class MyCache {
  constructor(isLocal = true) {
    this.storage = isLocal ? localStorage : sessionStorage
  }

  setItem(key, value) {
    if (typeof (value) === 'object') value = JSON.stringify(value)
    this.storage.setItem(key, value)
  }

  getItem(key) {
    try {
      return JSON.parse(this.storage.getItem(key))
    } catch (err) {
      return this.storage.getItem(key)
    }
  }

  removeItem(key) {
    this.storage.removeItem(key)
  }

  clear() {
    this.storage.clear()
  }

  key(index) {
    return this.storage.key(index)
  }

  length() {
    return this.storage.length
  }
}

const localCache = new MyCache()
const sessionCache = new MyCache(false)

export { localCache, sessionCache }
```

未完待续...
