---
title: Hexo用法笔记
date: 2018-07-20 20:09:54
tags:
- Hexo
---
## favicon 的配置

项目的 favicon 默认在你的博客根目录的 /source/img 下面，在 /source/img 下面添加 favicon.ico 即可，不要添加在主题文件夹内。

## 头像
_config.yml 配置
`sidebar-avatar: ./img/jiateng.jpeg`

## hexo安装

npm install hexo-cli -g

npm install hexo-server --save  Hexo 3.0 把服务器独立成了个别模块

npm install hexo-deployer-git --save 部署到git用的

hexo g 生成

hexo -d 部署 这个命令要用git bash运行

hexo g -d  生成部署

刷新网页没效果 hexo clean


## 文章概述

```
---
title: 优先队列元素是指针问题
date: 2016-12-12 22:54:41
tags:
-c++
---
```

## 代码块

```
{% codeblock [title] [lang:language] [url] [link text] %}
code snippet
{% endcodeblock %}
```

## 文章资源文件夹

设置

```
_config.yml
post_asset_folder: true
```
```
hexo new post_name 的时候生成post_name.md 的时候，也会生成一个post_name的文件夹，图片放里面，引用的时候![](post_name.png)
```

在本地浏览，把图片放到 source/images中,图片后缀重要大小写

## 图片靠左

```
<div align="left">
    ![](your.png)    
</div>
```
