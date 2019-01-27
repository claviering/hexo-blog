---
title: closure
date: 2019-01-27 22:06:09
tags:
- javascript
---
# 闭包

闭包是函数和声明该函数的词法环境的组合

```js
function init() {
    var name = "Mozilla"; // name 是一个被 init 创建的局部变量
    function displayName() { // displayName() 是内部函数,一个闭包
        alert(name); // 使用了父函数中声明的变量
    }
    displayName();
}
init();
```

`displayName` 可以访问到 `name` 的值

## 使用闭包的注意点
1. 由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除
2. 闭包会在父函数外部，改变父函数内部变量的值, 所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值

## 闭包的用途
1. 可以读取函数内部的变量
2. 让这些变量的值始终保持在内存中

## 为什么需要闭包呢

局部变量无法共享和长久的保存，而全局变量可能造成变量污染，所以我们希望有一种机制既可以长久的保存变量又不会造成全局污染。

## 何时使用

既想反复使用，又想避免全局污染

## ES6 解决闭包问题

var 只有全局作用域和函数作用域

let const 解决的 块级作用域

使用 let 代替 var 声明变量

### var

```js
var test = function () {
  var arr = []
  for(var i = 0; i < 5; i++){
    arr.push(function () {
      return i
    })
  }
  return arr
}

var test1 = test()
console.log(test1[0]()) // 5
console.log(test1[1]()) // 5
console.log(test1[2]()) // 5
```

### let

```js
var test = function () {
  const arr = []
  for(let i = 0; i < 5; i++){
    arr.push(function () {
      return i
    })
  }
  return arr
}

var test1 = test()
console.log(test1[0]()) // 0
console.log(test1[1]()) // 1
console.log(test1[2]()) // 2
```
## 总结

理解JavaScript的闭包是迈向高级JS程序员的必经之路，理解了其解释和运行机制才能写出更为安全和优雅的代码

## 参考

> [闭包](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures)

> [JavaScript 闭包 ](https://my.oschina.net/u/3693769/blog/1544436)

> [图解JS闭包](https://zhuanlan.zhihu.com/p/27857268)