---
layout: post
title: JS获取元素位置和视口大小等方法详解
categories: [Javascript]
description: 获取元素位置和视口大小等方法详解
keywords: Javascript, ReactNative
excerpt: 最近H5的项目中做了一些页面滚动顶部渐变和定位到对应的tab功能，就需要获取元素在视口里面的位置，滚动的距离等，同时最近rn项目也需要获取元素在视口里面的位置，就一起记录下
---

> 最近H5的项目中做了一些页面滚动顶部渐变和定位到对应的tab功能，就需要获取元素在视口里面的位置，滚动的距离等，同时最近rn项目也需要获取元素在视口里面的位置，就一起记录下，元素的含义及对用的参数自取

## js 获取参数含义

### getBoundingClientRect ( ) 返回值：对象 有6个属性

[MDN地址之getBoundingClientRect](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getBoundingClientRect)

```javascript
  let elem = document.querySelector('div');
  let rect = elem.getBoundingClientRect();
  for (var key in rect) {
    if(typeof rect[key] !== 'function') {
      let para = document.createElement('p');
      para.textContent  = `${ key } : ${ rect[key] }`;
      document.body.appendChild(para);
    }
  }
  // 得到的值 x : 146，y : 50，width : 440，height : 240，top : 50，right : 586，bottom : 290，left : 146 
  // left（元素左侧相对于可视区左上角的距离）, right（元素右侧相对于可视区左上角的距离）,top（元素上边相对于可视区左上角的距离）
  // bottom（元素下边相对于可视区左上角的距离）,width（可视宽度）,height（可视高度）
```

### 获取可视区域的宽和高
1. window.innerWidth 
2. indow.innerHeight
3. document.documentElement.clientWidth
4. document.documentElement.clientHeight

### 获取元素的属性
1. ffsetLeft （距离定位父级的距离）
2. offsetTop （距离定位父级的距离）
3. offsetWidth （可视宽度）
4. offsetHeight （可视高度）
5. clientLeft （左边框宽度）
6. clientTop （上边框宽度）
7. clientWidth（width + padding）
8. clientHeight（height + padding）
9. scrollTop（纵向滚动距离）
10. scrollLeft（横向滚动距离）
11. scrollWidth（内容宽度）
12. scrollHeight（内容高度）

### 获取屏幕宽和高
1. window.screen.width
2. window.screen,height

### 获取文档宽高
1. document.body.clientWidth
2. document.body.clientHeight
3. document.documentElement.scrollWidth
4. document.documentElement.scrollHeight
5. document.body.scrollWidth（如果内容宽度超过一屏，得到文档宽度；如果内容小于一屏，得到一屏的宽度）
6. document.body.scrollHeight （如果内容高度超过一屏，得到文档高度；如果内容小于一屏，得到一屏的高度）

### 获取滚动条距离
1. document.body.scrollTop
2. document.body.scrollLeft
3. window.scrollY
4. window.scrollX
5. document.documentElement.scrollTop
6. document.documentElement.scrollLeft
7. window.pageYOffset
8. window.pageXOffset


## React Native中测量组件和视口顶部之间的距离方法

measure()测量是根据view标签中的ref属性，使用代码如下

```javascript
class MyComponent extends React.Component {
  state = {
    containerHeight: 0
  };

  handleLayoutChange() {
    this.conainerView.measure(
      (x, y, width, height, left, top) => {
        // with：宽；height：高；left：x轴方向距离左边多少像素；top：y轴方向距离上边多少像素；
        this.setState({ containerHeight:height });
      }
    );
  }

  render() {
    return (
      <View
        onLayout={event => {
          this.handleLayoutChange(event);
        }}
        ref={view => {
          this.conainerView = view;
        }}
      >
        <Child containerHeight={this.state.containerHeight} />
      </View>
    );
  }
}
```
