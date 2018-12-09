---
title: proxy
date: 2018-12-09 11:08:13
tags:
- javascript
---

# Proxy 使用学习

Proxy, 代理, 在目标对象之前架设一层“拦截”, 外界对该对象的访问, 都必须先通过这层拦截, 因此提供了一种机制，可以对外界的访问进行过滤和改写. 

ES6 原生提供 Proxy 

## 基本使用
```js
/**
 * @params target 要拦截的目标对象
 * @params handler 定制拦截行为
*/
let p = new Proxy(target, handler)
```

## Proxy 支持的拦截操作一览，一共 13 种
1. get(target, propKey, receiver): 拦截对象属性的读取, 比如proxy.foo和proxy['foo']
2. set(target, propKey, value, receiver): 拦截对象属性的设置, 比如proxy.foo = v或proxy['foo'] = v, 返回一个布尔值
3. has(target, propKey): 拦截propKey in proxy的操作, 返回一个布尔值
4. deleteProperty(target, propKey): 拦截delete proxy[propKey]的操作, 返回一个布尔值
5. ownKeys(target): 拦截Object.getOwnPropertyNames(proxy)、Object.getOwnPropertySymbols(proxy)、Object.keys(proxy)、for...in循环, 返回一个数组. 该方法返回目标对象所有自身的属性的属性名，而Object.keys()的返回结果仅包括目标对象自身的可遍历属性
6. getOwnPropertyDescriptor(target, propKey): 拦截Object.getOwnPropertyDescriptor(proxy, propKey), 返回属性的描述对象
7. defineProperty(target, propKey, propDesc): 拦截Object.defineProperty(proxy, propKey, propDesc）、Object.defineProperties(proxy, propDescs)，返回一个布尔值. preventExtensions(target): 拦截
8. getPrototypeOf(target): 拦截Object.getPrototypeOf(proxy), 返回一个对象
9. isExtensible(target): 拦截Object.isExtensible(proxy), 返回一个布尔值
10. setPrototypeOf(target, proto): 拦截Object.setPrototypeOf(proxy, proto), 返回一个布尔值. 如果目标对象是函数, 那么还有两种额外操作可以拦截
11. apply(target, object, args): 拦截 Proxy 实例作为函数调用的操作, 比如proxy(...args)、proxy.call(object, ...args)、proxy.apply(...)
12. construct(target, args): 拦截 Proxy 实例作为构造函数调用的操作,比如new proxy(...args)

## 列子

```js
 let obj = {};
 let handler = {
   get(target, property) {
    console.log(`${property} 被读取`);
    return property in target ? target[property] : 3;
   },
   set(target, property, value) {
    console.log(`${property} 被设置为 ${value}`);
    target[property] = value;
   }
 }
 
 let p = new Proxy(obj, handler);
 p.name = 'tom' //name 被设置为 tom
 p.age; //age 被读取 3

```

## Proxy 实现双向数据绑定

```js
let dog = {
  name:"小黄",
  firends:[{
    name:"小红"
  }]
}

let proxy = new Proxy(dog,{
    get (target,property) {
        console.log('get被监控到了')
        return target[property]
    },
    set (target,property,value) {
        console.log('set被监控到了')
        target[property] = value
    }
})
proxy.name = '小红' // 打印输出 'set被监控到了'
proxy.name // 打印输出 'get被监控到了'
```

## 下面的例子使用get拦截，实现数组读取负数的索引

```js
function createArray(...elements) {
  let handler = {
    get(target, propKey, receiver) {
      let index = Number(propKey);
      if (index < 0) {
        propKey = String(target.length + index);
      }
      return Reflect.get(target, propKey, receiver);
    }
  };
  let target = [];
  target.push(...elements);
  return new Proxy(target, handler);
}
let arr = createArray('a', 'b', 'c');
arr[-1] // c
```