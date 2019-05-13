---
title: css-1px
date: 2019-05-13 07:59:48
tags:
- css
---

## 摘要

区分物理像素、逻辑像素、DPR(Device Pixel Ratio，dpr = 物理像素数 / 逻辑像素数)，更好理解移动端适配，显示出真正的 1px

## 名词解释

- 物理像素(DP, device pixels):

显示屏是由一个个物理像素点组成的，通过控制每个像素点的颜色，使屏幕显示出不同的图像，屏幕从工厂出来那天起，它上面的物理像素点就固定不变了，单位pt。比如 iphone7 分辨率 750*1334 指的是物理像素

- 逻辑像素(虚拟像素 PX CSS pixels):

虚拟的，css 使用的就是逻辑像素，视口大小 375*667 说的是逻辑像素

- DPR:

dpr = 物理像素数 / 逻辑像素数，在移动开发中1个css像素占用多少设备像素。比如 iphone7 的 DPR = 750 / 375 = 2。所以编程的时候 1px CSS像素实际显示为 2px 设备像素，0.5 px CSS像素实际显示为 1px 设备像素

## 参考

> [jawil/blog](https://github.com/jawil/blog/issues/21)
> 
> [一篇文章告诉你 1px 等于多少 cm](https://juejin.im/post/5cb5dc95e51d456e2b15f5f3)
> 
> [移动端1px解决方案](https://juejin.im/post/5c8ba122e51d4574cf120378)