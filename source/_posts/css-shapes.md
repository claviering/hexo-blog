---
title: css-shapes
date: 2019-05-12 13:25:22
tags:
- css
---
<link href="main.css" rel="stylesheet"></link>

## 摘要

用 css 改变元素的形状，超酷，前端切图仔必备

## Shapes from box values

css 形状盒模型

- content-box
- padding-box
- border-box
- margin-box

## Basic Shapes

- inset 插入一个长方形
- circle 圆形
- ellipse 椭圆
- polygon 多边形

### Usage

关键词

- closest-side 在当前盒模型最近的一边
- farthest-side 在当前盒模型最远的一边

### circle

circle(shape-radius) 或者 circle(shape-radius at position)

```css
.box-circle::before {
  content: "";
  float: left;
  width: 350px;
  height: 350px;
  shape-outside: circle(50% at top left);
  border-radius: 50%;
}
```

<div class="box-circle">
  <p style="text-indent: 0;">One November night in the year 1782, so the story runs, two brothers sat over their winter fire in the little French town of Annonay, watching the grey smoke-wreaths from the hearth curl up the wide chimney. Their names were Stephen and Joseph Montgolfier, they were papermakers by trade, and were noted as possessing thoughtful minds and a deep interest in all scientific knowledge and new discovery. Before that night—a memorable night, as it was to prove—hundreds of millions of people had watched the rising smoke-wreaths of their fires without drawing any special inspiration from the fact.</p>
</div>


### inset

inset(top, right, bottom, left, border-radius)

```css
.shape {
  float: left;
  shape-outside: inset(20px 10px 20px 10px round 10px);
}
```

<div class="box-inset">
  <p style="text-indent: 0;">One November night in the year 1782, so the story runs, two brothers sat over their winter fire in the little French town of Annonay, watching the grey smoke-wreaths from the hearth curl up the wide chimney. Their names were Stephen and Joseph Montgolfier, they were papermakers by trade, and were noted as possessing thoughtful minds and a deep interest in all scientific knowledge and new discovery. Before that night—a memorable night, as it was to prove—hundreds of millions of people had watched the rising smoke-wreaths of their fires without drawing any special inspiration from the fact.</p>
</div>

### ellipse

```css
.shape {
    float: left;
    shape-outside: ellipse(40% 50% at left);
    margin: 20px;
    width: 100px;
    height: 200px;
}
```
<div class="box-ellipse">
  <p style="text-indent: 0;">One November night in the year 1782, so the story runs, two brothers sat over their winter fire in the little French town of Annonay, watching the grey smoke-wreaths from the hearth curl up the wide chimney. Their names were Stephen and Joseph Montgolfier, they were papermakers by trade, and were noted as possessing thoughtful minds and a deep interest in all scientific knowledge and new discovery. Before that night—a memorable night, as it was to prove—hundreds of millions of people had watched the rising smoke-wreaths of their fires without drawing any special inspiration from the fact.</p>
</div>

### polygon

```css
.shape {
    float: left;
    shape-outside: polygon(0px 0px, 0px 189px, 100.48% 94.71%, 200px 120px, 80.67% 37.17%);
    width: 200px;
    height: 200px;
}
```

<div class="box-polygon">
  <p style="text-indent: 0;">One November night in the year 1782, so the story runs, two brothers sat over their winter fire in the little French town of Annonay, watching the grey smoke-wreaths from the hearth curl up the wide chimney. Their names were Stephen and Joseph Montgolfier, they were papermakers by trade, and were noted as possessing thoughtful minds and a deep interest in all scientific knowledge and new discovery. Before that night—a memorable night, as it was to prove—hundreds of millions of people had watched the rising smoke-wreaths of their fires without drawing any special inspiration from the fact.</p>
</div>

## Shapes From Images

直接用图片做形状

```css
img {
  float: left;
  shape-outside: url(../images/star-shape1.png);
  shape-margin: 20px;
  shape-image-threshold: .2;
}
```
shape-margin 外边距

shape-image-threshold 图片透明度。如果原始图片透明度不是 1，需要设置这个值，不然 css shapes 不起效果

不显示图片的效果

```css
.box::before {
    content: "";
    float: left;
    width: 400px;
    height: 300px;
    shape-outside: url(../images/star-shape-large.png);
    shape-image-threshold: .3;
}
```
## Creating shapes using a gradient

使用颜色梯度创建 css shapes

```css
.box::before {
    content: "";
    float: left;
    height: 250px;
    width: 400px;
    background-image: radial-gradient(ellipse closest-side, rebeccapurple, blue 50%, transparent);
    shape-outside: radial-gradient(ellipse closest-side, rebeccapurple, blue 50%, transparent);
    shape-image-threshold: .3;
}
```

## Tools

[在线编辑 css 形状](https://bennettfeely.com/clippy/)

## 参考

> [Web技巧 (04)](https://zhuanlan.zhihu.com/p/63412563)
> 
> [盒模型](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Shapes/From_box_values)
> 
> [基础形状](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Shapes/Basic_Shapes)