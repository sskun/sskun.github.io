---
layout: post
title: Javascript实现输入框插入自定义文本和复制选中的或者指定的文本内容
categories: [Javascript]
description: Javascript实现输入框插入自定义文本和复制选中的或者指定的文本内容
keywords: 前端博客, 复制文本, 输入框插入, 文本框插入, 文本框输入
---

之前项目里面实现输入框动态插入宏和复制文本到粘贴板，记录一下

#### 动态插入文本

```javascript
export const insertInputVal = ({ id, value }) => {
  var myField = document.getElementById(id)
  let newVal = ''
  if (myField.selectionStart || myField.selectionStart === 0) {
    var startPos = myField.selectionStart
    var endPos = myField.selectionEnd
    myField.focus()
    myField.setSelectionRange(endPos + value.length, endPos + value.length)
    newVal = myField.value.substring(0, startPos) + value + myField.value.substring(endPos, myField.value.length)
  } else {
    newVal = myField.value += value
  }
  return newVal
}
```

#### 复制指定文本到粘贴板
```javascript
// 前端拷贝函数
export function webCopy(value) {
  if (window.clipboardData && window.clipboardData.setData) {
    return window.clipboardData.setData('Text', value)
  } else if (document.queryCommandSupported && document.queryCommandSupported('copy')) {
    let ele = document.createElement('input')
    ele.value = value
    document.body.appendChild(ele)
    ele.select()
    document.execCommand('copy')
    document.body.removeChild(ele)
  }
}
```
