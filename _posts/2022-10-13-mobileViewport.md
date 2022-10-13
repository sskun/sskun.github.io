---
layout: post
title: 移动端各种分辨率手机屏幕----适配方法集锦
categories: [Javascript]
description: 主要记录H5页面在移动端适配方案，包括px,rem，vh等等
keywords: rem,viewport
---
### meta标签 使用viewport
简单粗暴的方案，设计稿按照750的，设计稿测的px直接写即可

```
<meta name="viewport" id="viewport" content="target-densitydpi=device-dpi,width=750,user-scalable=no">
```

### rem方案
