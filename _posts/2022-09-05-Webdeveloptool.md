---
layout: post
title: 前端开发工作中使用的工具使用记录和配置方法
categories: [Tool]
description: vscode
keywords: vscode,开发工具
---

工欲善其事必先利其器，开发过程离不开工具，熟悉工具的配置方法对开发人员来说会事半功倍，所以本文主要是记录一些惊颤用的工具的配置方法和插件使用，让大家配置一个自己顺手的开发工具

## 代码开发神器，前端必用工具-vscode
### vscode插件推荐列表

#### 1、自动格式化插件：Prettier - Code formatter
[Prettier文档地址](https://prettier.io/docs/en/configuration.html)

配置Prettie规则

项目根目录文件 prettier.config.js，一般放在项目里面可以统一一个项目的代码格式

```javascript
module.exports = {
  "prettier.printWidth": 100, // 超过最大值换行
 "prettier.tabWidth": 4, // 缩进字节数
 "prettier.useTabs": false, // 缩进不使用tab，使用空格
 "prettier.semi": true, // 句尾添加分号
 "prettier.singleQuote": true, // 使用单引号代替双引号
 "prettier.proseWrap": "preserve", // 默认值。因为使用了一些折行敏感型的渲染器（如GitHub comment）而按照markdown文本样式进行折行
 "prettier.arrowParens": "avoid", // (x) => {} 箭头函数参数只有一个时是否要有小括号。avoid：省略括号
 "prettier.bracketSpacing": true, // 在对象，数组括号与文字之间加空格 "{ foo: bar }"
 "prettier.disableLanguages": ["vue"], // 不格式化vue文件，vue文件的格式化单独设置

 "prettier.endOfLine": "auto", // 结尾是 \n \r \n\r auto

 "prettier.eslintIntegration": false, //不让prettier使用eslint的代码格式进行校验

 "prettier.htmlWhitespaceSensitivity": "ignore",

 "prettier.ignorePath": ".prettierignore", // 不使用prettier格式化的文件填写在项目的.prettierignore文件中

 "prettier.jsxBracketSameLine": false, // 在jsx中把'>' 单独放一行

 "prettier.jsxSingleQuote": false, // 在jsx中使用单引号代替双引号

 "prettier.parser": "babylon", // 格式化的解析器，默认是babylon

 "prettier.requireConfig": false, // Require a 'prettierconfig' to format prettier

 "prettier.stylelintIntegration": false, //不让prettier使用stylelint的代码格式进行校验

 "prettier.trailingComma": "es5", // 在对象或数组最后一个元素后面是否加逗号（在ES5中加尾逗号）

 "prettier.tslintIntegration": false // 不让prettier使用tslint的代码格式进行校验
 "trailingComma": "none" // 函数最后不需要逗号
}
```

设置settings.json方式 

```
"prettier": {
    "printWidth": 300, // 代码宽度  js超过 300换行
    "bracketSameLine": true,
    "trailingComma": "none", //禁止随时添加逗号,这个很重要。找了好久
    "singleQuote": true, // 单引号不自动转换双引号
    "semi": false, // 不添加分号
    "proseWrap": "preserve", // 代码超出是否要换行 preserve保留
    "arrowParens": "avoid", // 箭头函数一个参数不加括号
  }

  // 或者

  "prettier.semi": false ,
  "prettier.singleQuote": true ,
  "prettier.trailingComma": "none" ,
```
#### 2、vscode操作Git插件 ：Git History +  GitLens

#### 3、Eslint插件：Eslint

#### 4、文件图标：Material Icon Theme


### vscode 配置项文件 settings.json

>格式化快捷键：Windows：Shift + Alt + F。  mac：Shift + Option + F

```javascript
{ 
    "editor.tabSize": 2,
    "files.associations": {
      "*.vue": "vue"
    },
    "search.exclude": {
      "**/node_modules": true,
      "**/bower_components": true,
      "**/dist": true
    },
    "emmet.syntaxProfiles": {
      "javascript": "jsx",
      "vue": "html",
      "vue-html": "html"
    },
    "editor.formatOnSave": true, // 保存格式化代码
    "editor.fontSize": 12, // 文本字体大小
    "editor.wordWrap": "on", // 是否自动换行
    "files.autoSave": "off", // off  afterDelay  onFocusChange(当编辑器失去焦点时，将自动保存为保存的编辑器) onWindowChange（将自动保存为保存的编辑器，A页面切换到B页面）
    "files.autoSaveDelay": 1000, // 默认1000，控制自动保存具有未保存更改的编辑器之前的延迟(以毫秒为单位) iles.autoSave设置afterDelay有效
    "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode" // js 文件默认使用prettier格式化
    },
    "[html]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode" // html 格式化
    },
     "[css]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[less]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "git.mergeEditor":false, //打开当前冲突的状态的文件编辑器
    "eslint.format.enable": true,// 是否看起eslint
    "editor.codeActionsOnSave": { 
        "source.organizeImports": true, //自动调整 import 语句相关顺序，能够让你的 import 语句按照字母顺序进行排列
    },
    "git.confirmSync": false,
    "editor.renderWhitespace": "boundary",
    "editor.cursorBlinking": "smooth",
    "editor.minimap.enabled": true,
    "editor.minimap.renderCharacters": false,
    "prettier.semi": false ,
    "prettier.singleQuote": true ,
    "prettier.trailingComma": "none" ,
    "window.title": "${dirty}${activeEditorMedium}${separator}${rootName}",
    "window.zoomLevel": 0,
    "editor.codeLens": true,
    "editor.snippetSuggestions": "top",
    "security.workspace.trust.untrustedFiles": "open",
}
```
暂时先按照这个配置设置，不懂的属性可以在 vscode 设置里面搜索属性值，会有详细介绍
