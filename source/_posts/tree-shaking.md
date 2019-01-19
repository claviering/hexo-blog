---
title: tree-shaking
date: 2019-01-19 10:06:29
tags:
- js
- css
---

# tree-shaking

前端中的tree-shaking可以理解为通过工具"摇"我们的JS文件，将其中用不到的代码"摇"掉，是一个性能优化的范畴

webpack 官网 [tree-shaking](https://webpack.js.org/guides/tree-shaking/)

配置 package.json

```js
{
  "name": "your-project",
  "sideEffects": [
    "./src/some-side-effectful-file.js",
    "*.css"
  ]
}
```

## JS Tree-shaking

- 代码不会被执行，不可到达
- 代码执行的结果不会被用到
- 代码只会影响死变量（只写不读）

## CSS Tree-shaking

使用 postCSS

整体思路是这样的，遍历所有的css文件中的selector选择器，然后去所有js代码中匹配，如果选择器没有在代码出现过，则认为该选择器是无用代码

## 参考

> [Tree-Shaking性能优化实践 - 原理篇](https://juejin.im/post/5a4dc842518825698e7279a9)

> [Tree-Shaking性能优化实践 - 实践篇](https://juejin.im/post/5a4dca1d518825128654fa78)