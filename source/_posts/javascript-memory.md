---
title: javascript-memory
date: 2019-01-20 19:48:45
tags:
- javascript
---

# javascript 中的内存

在 JS 中, 没有专门的内存管理接口, 所有的内存管理都是"自动"的. JS 在创建变量时, 自动分配内存, 并在不使用的时候, 自动释放

JS内存空间分为栈(stack)、堆(heap)、池(一般也会归类为栈中)。 其中栈存放变量，堆存放复杂对象，池存放常量。

## 内存生命周期

Allocate memory -> Use memory -> Release memory

## JS 内存回收算法

### 引用计数垃圾收集
  如果没有引用指向该对象, 对象将被垃圾回收机制回收
### 标记-清除内存回收算法
  这个算法把“对象是否不再需要”简化定义为“对象是否可以获得”


## 内存泄露

没有及时释放不再用到的内存

- 全局变量
- 未销毁的定时器和回调函数
- 闭包
- DOM 引用

## 垃圾回收机制

引用数为 0

```js
let arr = [1, 2, 3, 4];
console.log('hello world');
arr = null;
```

## ES6 WeakMap WeakSet

`WeakMap` 只接受对象作为键名（`null`除外），不接受其他类型的值作为键名

`WeakMap`的键名所指向的对象，不计入垃圾回收机制

`WeakMap`只有四个方法可用：`get()`、`set()`、`has()`、`delete()`

`WeakSet` 类似

## 参考

> [JavaScript 内存泄漏教程](http://www.ruanyifeng.com/blog/2017/04/memory-leak.html)

> [精读《JS 中的内存管理》](https://zhuanlan.zhihu.com/p/30552148)

> [内存管理](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Memory_Management)