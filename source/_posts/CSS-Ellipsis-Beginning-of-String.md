---
title: CSS-Ellipsis-Beginning-of-String
date: 2019-06-20 15:52:05
tags:
- css
---

CSS 实现超出盒子大小，省略号出现在左边

<div class="box">
  <span class="content">Demo: CSS Ellipsis Beginning of String</span>
</div>

## 参考

> [CSS Ellipsis Beginning of String](https://davidwalsh.name/css-ellipsis-left)

<style>
.box{
  width: 200px;
  height: 20px;
  direction: rtl;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  text-indent: 0px;
}
.box br{
    display: none;
  }
.box span{
  text-indent: 0px;
}
</style>
