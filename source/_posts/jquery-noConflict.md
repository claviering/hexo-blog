---
title: jquery moConflict 函数原理
date: 2020-11-30 21:29:05
tags:
- jquery
- 源码阅读
---

jQuery noConflict 函数

作用: 不占用 $ 和 jQuery 变量名，返回当前的 jQuery，可以保存保存到其他自定义变量名

```js
(function (global, factory) {
  // 省略其他代码

  // Pass this if window is not defined yet
})(typeof window !== "undefined" ? window : this, function (window, noGlobal) {
  // 省略其他代码
  var

    // Map over jQuery in case of overwrite
    _jQuery = window.jQuery,

    // Map over the $ in case of overwrite
    _$ = window.$;

  jQuery.noConflict = function (deep) {
    if (window.$ === jQuery) {
      window.$ = _$;
    }

    if (deep && window.jQuery === jQuery) {
      window.jQuery = _jQuery;
    }

    return jQuery;
  };
  if (!noGlobal) {
    window.jQuery = window.$ = jQuery;
  }
  return jQuery;
});
```

## 原理

`_jQuery = window.jQuery`
如果有 jQuery 变量被使用，则保存 jQuery 变量到 `_jQuery` 变量，否则 `_jQuery` 为 `Undefined` 

`_$ = window.$`
如果有 $ 变量被使用，则保存 $ 变量到 `_$`，否则 `_$` 为 `Undefined`

```js
if (!noGlobal) {
  window.jQuery = window.$ = jQuery;
}
```
jQuery 执行到最后，`window.jQuery = window.$ = jQuery;` 全局安装 jQuery，占用 $ 和 jQuery 变量。

通过调用 noConflict 函数，`window.$ === jQuery`，表达式为 true，因为执行了 `window.jQuery = window.$ = jQuery;`， `window.$ = _$`，则从 `_$` 恢复 `$`

`deep && window.jQuery === jQuery` 调用 `noConflict(true)`，表达式为 true，因为执行了 `window.jQuery = window.$ = jQuery;`，则从 `_jQuery` 恢复 旧的 `jQuery`

最后 `return jQuery`，返回当前 jQuery，用户可以保存到其他自定义变量中