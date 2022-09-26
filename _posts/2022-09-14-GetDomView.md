---
layout: post
title: JS获取元素位置和视口大小等方法详解
categories: [Javascript]
description: 获取元素位置和视口大小等方法详解
keywords: Javascript, ReactNative
excerpt: 最近H5的项目中做了一些页面滚动顶部渐变和定位到对应的tab功能，就需要获取元素在视口里面的位置，滚动的距离等，同时最近rn项目也需要获取元素在视口里面的位置，就一起记录下
---

## React Native中测量组件和视口顶部之间的距离方法

measure()测量是根据view标签中的ref属性

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
