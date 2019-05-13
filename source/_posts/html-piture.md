---
title: 响应式图片
date: 2019-05-12 19:18:00
tags:
- html
- css
---

## 摘要

移动端响应式图片，节省流量，提高用户体验，主要使用媒体查询。一句话就是，给你的用户提供正确的图像

## 最简单

```css
img {
  max-width: 100%;
  height: auto;
}
```
问题: 浪费流量

## img

使用两个新属性 `srcset` 和 `sizes`

```html
<img srcset="elva-fairy-320w.jpg 320w,
             elva-fairy-480w.jpg 480w,
             elva-fairy-800w.jpg 800w"
     sizes="(max-width: 320px) 280px,
            (max-width: 480px) 440px,
            800px"
     src="elva-fairy-800w.jpg" alt="Elva dressed as a fairy">
```

srcset: 定义图片供浏览器选择
- 图片名字
- 空格
- 图片宽度

sizes: 定义媒体查询，选择什么图片
- 媒体条件
- 空格
- 当媒体条件为真时，图像将填充的插槽宽度

浏览器工作流程

获取设备宽度 -> 选择 `sizes` -> 查找指定插槽大小 -> 加载 `srcset` 中最接近插槽大小的图片

不兼容的旧浏览器版本，会忽略 `srcset` 和 `sizes` 直接加载 src 资源

## picture 标签

不用分辨率加载不同图片

```html
<picture>  
    <source srcset="large.jpg" media="(min-width: 800px)">  
    <source srcset="medium.jpg" media="(min-width: 600px)">  
    <img srcset="small.jpg">  
</picture>  
```

注意: media 和 sizes 不能同时使用

## 使用现代图像格式

新的图片格式，比如 WebP 和 jpeg-2000，a low file size and high quality at the same time，但是有的浏览器不支持

支持不同图片格式

```html
<picture>
  <source type="image/svg+xml" srcset="pyramid.svg">
  <source type="image/webp" srcset="pyramid.webp"> 
  <img src="pyramid.png" alt="regular pyramid built from four equilateral triangles">
</picture>
```

## 配合

不同宽度，选择不同 source
同一宽度，选择同一 source，不同设备像素比，选择不同图片，选择图片清晰度。

```html
<picture>
	<source media="(max-width:500px)" srcset="example-phone.jpg 500w,example-HD-phone.jpg 1000w" sizes="100vw">
	<source media="(max-width:1000px)" srcset="example.jpg 500w,example-HD.jpg 1000w" sizes="50vw">
<img src="example.jpg" alt="a house with a big courtyard">
</picture>
```

## 为什么不用 css 或者 js

当浏览器开始加载页面时，它会在主解析器开始加载和解释页面的CSS和JavaScript之前开始下载（预加载）任何图像。 这是一项非常有用的技术，平均减少了20％的页面加载时间。 但是，它对响应式图像没有帮助，因此需要实现像srcset这样的解决方案。 例如，您无法加载<img>元素，然后使用JavaScript检测视口宽度，并根据需要动态地将源图像更改为较小的图像。 到那时，原始图像已经被加载，你也会加载小图像，这在响应图像方面更差。

## 参考

> [响应式图片](https://juejin.im/post/5ccfcfd06fb9a0322b5c0d21)
> 
> [Responsive images](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)