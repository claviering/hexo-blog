---
title: infinite-scroll 无限滚动
date: 2019-07-21 10:09:00
tags:
- javascript
---

# infinite-scroll 无限滚动

- scrollTop: 滚动视窗的高度距离window顶部的距离，它会随着往上滚动而不断增加，初始值是0，它是一个变化的值；
- clientHeight: 它是一个定值，表示屏幕可视区域的高度；
- scrollHeight: 页面不能滚动时是不存在的，body长度超过window时才会出现，所表示body所有元素的长度，

由上面的三个值所产生一个原理公式：

scrollTop + clientHeight >= scrollHeight


    let clientHeight  = document.documentElement.clientHeight; //浏览器高度
    let scrollHeight = document.body.scrollHeight;
    let scrollTop = document.documentElement.scrollTop;
 
    let distance = 50;  //距离视窗还用50的时候，开始触发；

    if ((scrollTop + clientHeight) >= (scrollHeight - distance)) {
        console.log("到底了，开始加载数据");
    }


## Demo

<ul id='infinite-list'>
</ul>

## 参考

> [Infinite Scroll](https://codepen.io/anon/pen/ydPwRe)

> [js如何实现上拉加载更多](https://segmentfault.com/a/1190000017078193)

<script>
var listElm = document.querySelector('#infinite-list');

// Add 20 items.
var nextItem = 1;
var loadMore = function() {
  for (var i = 0; i < 20; i++) {
    var item = document.createElement('li');
    item.innerText = 'Item ' + nextItem++;
    listElm.appendChild(item);
  }
}

// Detect when scrolled to bottom.
listElm.addEventListener('scroll', function() {
  if (listElm.scrollTop + listElm.clientHeight >= listElm.scrollHeight) {
    loadMore();
  }
});

// Initially load some items.
loadMore();
</script>

<style>
#infinite-list {
  /* We need to limit the height and show a scrollbar */
  width: 200px;
  height: 300px;
  overflow: auto;

  /* Optional, only to check that it works with margin/padding */
  margin: 30px;
  padding: 20px;
  border: 10px solid black;
}

/* Optional eye candy below: */
#infinite-list li {
  padding: 10px;
  list-style-type: none;
}
#infinite-list li:hover {
  background: #ccc;
}
</style>