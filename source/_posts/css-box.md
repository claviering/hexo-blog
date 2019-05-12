---
title: css 盒模型
date: 2019-05-12 09:30:56
tags:
- css
---

## 摘要

CSS + div 基于盒模型的布局，准确控制标签大小

## 盒模型

盒模型分为 W3C 标准盒模型和IE盒模型，默认是W3C标准盒模型，IE8+ 浏览器可以使用 `box-sizing` 控制盒模型

1. box-sizing IE盒模型
2. content-box W3C 标准盒模型

不管哪种模型 margin 都不计算进盒模型大小

### IE盒模型

注意: border 和 padding 需要同时计算上下或者左右

    width  = border + padding + content
    height = border + padding + content

盒子实际大小 = width * height

```css
width: 200px;
height: 200px;
background-color: red;
padding: 40px;
border: 40px solid;
margin: 20px;
box-sizing: border-box;
```
width/height > (border + padding) 盒子实际大小为: width * height = 200px

当 设置 width/height < border + padding 时，盒子实际大小不是 width * height，而是 (border + padding) * (border + padding)

```css
width: 100px;
height: 100px;
background-color: red;
padding: 40px;
border: 40px solid;
margin: 20px;
box-sizing: border-box;
```
盒子实际大小为: (border + padding) * (border + padding) = 160px

### W3C 标准盒模型

    width  = content
    height = content

盒子实际大小 = (width + border + padding) * (height + border + padding)，开发中一般是这个。