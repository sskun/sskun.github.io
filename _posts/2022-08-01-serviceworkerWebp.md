---
layout: post
title: 使用Service Workers技术 让网站响应式加载webp格式图片
categories: [性能优化, javascript]
description:
keywords: webp, Service Workers, Service, 性能优化
---

图片在现在的网站上随处可见且被广泛应用，所以优化图片可以对网站性能优化有很重要的帮助。相对于我们传统的 PNG/JPG 等格式图片，webp 格式的图片可以大大降低 size，但是 webp 存在兼容性，目前，Chrome、Opera 以及 Android 能够支持 WebP 格式，但 Safari 和 IE 尚未支持

## Service Workers 技术实现响应式加载 webp 格式图片

我们采用开发者工具观察 HTTP 请求头部，可以看出可以根据 Accept 头部来判断我们的浏览器是否支持 WebP 图片

![image](https://kunyk.gitee.io/sansssimg/images/servicework/webp01.jpg)

根据这个 Request Headers 里面的 Accept，我们可以判断是否支持使用 webp 格式的图片。我们需要注册一个 Service Worker。Service Worker 的一大特性就是，它们能够拦截网络请求，这样子，我们就能够完全控制响应内容。使用这个特性，我们能够监听 HTTP 头部，并决定如何做。

```javascript
// Register the service worker
if ('serviceWorker' in navigator) {
  navigator.serviceWorker
    .register('./service-worker.js')
    .then(function (registration) {
      // Registration was successful
      console.log(
        'ServiceWorker registration successful with scope: ',
        registration.scope
      );
    })
    .catch(function (err) {
      // registration failed :(
      console.log('ServiceWorker registration failed: ', err);
    });
}
```

上面代码我们首先做了一个简单的检查，判断浏览器是否支持 Service Worker，如果支持，注册并安装 Service Worker。这段代码代码最好的地方就是做了兼容处理，如果浏览器不支持 Service Workers，它们会自动回退并且用户不会注意到其中差别

接下来，我们需要创建 Service Worker 文件 service-worker.js，用于拦截正在传递到服务器的请求

```javascript
'use strict';

// Listen to fetch events
self.addEventListener('fetch', function (event) {
  // Clone the request
  var req = event.request.clone();

  // Check if the image is a jpeg
  if (/\.jpg$|.png$/.test(event.request.url)) {
    // Get all of the headers
    let headers = Array.from(req.headers.entries());

    // Inspect the accept header for WebP support
    var acceptHeader = headers.find((item) => item[0] == 'accept');
    var supportsWebp = acceptHeader[1].includes('webp');

    // If we support WebP
    if (supportsWebp) {
      // Build the return URL
      var returnUrl = req.url.substr(0, req.url.lastIndexOf('.')) + '.webp';

      event.respondWith(
        fetch(returnUrl, {
          mode: 'no-cors',
        })
      );
    }
  }
});
```

添加一个事件监听器来监听任何一个 fetch 事件。当每个请求发生时，先判断当前的请求是否是获取 JPEG 或者 PNG 格式的图片。如果当前的请求是获取图片，我就能根据 HTTP 请求头部来决定最佳的响应。在这种情况下，我通过检查 Accept 头部并且查找是否存在“image/webp“ Mime 类型。一旦查询完头部的值，我就能确定浏览器是否支持 WebP 图片，如果浏览器支持 WebP 图片，就返回相应的 WebP 图片。
