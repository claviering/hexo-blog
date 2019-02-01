---
title: FLIP
date: 2019-01-31 17:22:20
tags:
- css
- js
- 动画
---

# FLIP (First, Last, Invert, Play)

FLIP技术可以以一种高性能的方式来动态的改变DOM元素的位置和尺寸，而不需要管它的布局是如何计算或渲染的. 在改变的过程中将赋予一定的动效，从而达到我们所需要的目的，让UI动效更为合理，相应增强用户的体验

任何触发布局变化的属性（比如height），浏览器都会递归检查布局中的其他元素是否也因此改变，这样的一个过程花销是很贵的

在动画中尽量的只使用transform和opacity, 让动效更流畅，让样式计算的数量尽量的少，而且尽可能的快

## First
First，指的是在任何事情发生之前（过渡之前），记录当前元素的位置和尺寸。可以使用`getBoundingClientRect()`这个API来处理
```js
// 获取当前元素的边界 
const first = el.getBoundingClientRect()
```

## Last
执行一段代码，让元素发生相应的变化，并记录元素在最后状态的位置和尺寸

```js
// 通过给元素添加一个类名，设置元素最后状态的位置和大小 （在.totes-at-the-end中添加相应的样式规则）
// 布局发生了变化
el.classList.add('totes-at-the-end')

// 记录元素最后状态的位置和尺寸大小
const last = el.getBoundingClientRect()
```
## Invert
通过 transform 来改变元素的位置和尺寸, 从而创建它位于初始位置的一个错觉

## Play
把 transform 设置为 none, 将其移动到 last 位置

## flipping.js

FLIP 函数库

[flipping.js](https://github.com/davidkpiano/flipping)

## 参考

> [FLIP技术给Web布局带来的变化](https://www.w3cplus.com/javascript/animating-layouts-with-the-flip-technique.html)