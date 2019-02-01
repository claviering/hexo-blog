---
title: css-animation
date: 2019-02-01 09:17:36
tags:
- css
- js
- 动画
---
# WEB动画API

`Element.animate()`

## Syntax

`let animation = element.animate(keyframes, options);`

## return value

Returns an `Animation`.

### 当前动画状态

`animation.playState`

### 修改动画的当前状态
```js
animation.pause(); //"paused"
animation.play();  //"running"
animation.cancel(); //"idle"... 跳到初始状态
animation.finish(); //"finished"...跳到结束状态
```
### 播放速度

`animation.playbackRate = 2`

### 结束回调
`animation.onfinish = function(){}`

### reverse

反转动画

`animation.reverse();`


## js 列子

```js
let player = document.getElementById('toAnimate').animate([
  { transform: 'scale(1)', opacity: 1, offset: 0 },
  { transform: 'scale(.5)', opacity: .5, offset: .3 },
  { transform: 'scale(.667)', opacity: .667, offset: .7875 },
  { transform: 'scale(.6)', opacity: .6, offset: 1 }
], {
  duration: 700, //milliseconds
  easing: 'ease-in-out', //'linear', a bezier curve, etc.
  delay: 10, //milliseconds
  iterations: Infinity, //or a number
  direction: 'alternate', //'normal', 'reverse', etc.
  fill: 'forwards' //'backwards', 'both', 'none', 'auto'
});
```
## 等效 css 动画

```css
@keyframes emphasis {
  0% {
    transform: scale(1); 
    opacity: 1; 
  }
  39% {
    transform: scale(.5); 
    opacity: .5; 
  }
  78.75% {
    transform: scale(.667); 
    opacity: .667; 
  }
  100% {
    transform: scale(.6);
    opacity: .6; 
  }
}
#toAnimate {
  animation: emphasis 700ms ease-in-out 10ms infinite alternate forwards;
}
```
## 多个动画

给同一个 dom 绑定多个动画

## 参考

> [WEB动画API](https://www.w3cplus.com/blog/tags/521.html)

> [MND](https://developer.mozilla.org/en-US/docs/Web/API/Element/animate)