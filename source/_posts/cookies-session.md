---
title: cookie_session
date: 2018-12-31 12:06:24
tags:
- cookies
- session
---


# 整理 cookies session 知识

## Cookie 是什么?  
它是一种浏览器本地存储的一种方式.可以将一部分资源存放在本地,已达到更好的网络体验.

API 操作 Cokkie: document.cookie  
存储大小: 4KB  
不同浏览器对 Cookie 数量和大小的限制，是不一样的  
Cookie 共享: 浏览器的同源策略, 协议相同 主机相同 端口号相同

## Cookie 与 HTTP 协议

### HTTP 回应: Cookie 生成

服务器如果希望在浏览器保存 Cookie，就要在 HTTP 回应的头信息里面，放置一个Set-Cookie字段

`Set-Cookie:foo=bar`

可以附加 Cookie 属性: Expires=<date>; Max-Age=<>; Domain=<>; Path=<>; Secure; HttpOnly;

Set-Cookie 只要有一个属性不同, 就会生成一个全新的 Cookie, 而不是替换原来的 Cookie, 下次访问, 浏览器将发送两个 Cookie

### HTTP 请求: Cookie 发送
浏览器想服务器发送 HTTP 请求时, 每个请求都会带上 Cookie

`Cookie: foo=bar`

服务器无法知道收到的 Cookie 的各种属性, 何时过期等  
哪个域名设置的 Cookie

## Session

服务器端技术, 用来保存用户的回话信息  
有状态的, 需要浏览器通知服务器关闭 Session

## SSO (Single Sign On)

### 普通的登录认证机制
填写用户名和密码后, 完成登录认证  
Session 中标记登录状态为 yes  
同时浏览器中写入 Cookie, 这个 Cookie 是这个用户的唯一标识, 下次请求的时候带上这个 Cookie, 服务器根据 Cookie 找到对应的 session, 判断用户是否登录

### 同域下的 SSO

在 sso.example.com 登录  
sit1.example.com 和 sit2.example.com 也都登录了  
在sso.example.com 服务端的 session中记录了登录状态, 同时浏览器的 sso.example.com 下写入 Cookie  
思考  
sit1.example.com 和 sit2.example.com 怎么登陆?

问题  
1. Cookie 是不能跨域的，我们 Cookie 的 domain 属性是sso.example. sit1.example.com和 sit2.example.com 发送请求是带不上的
2. sso、sit1 和 sit2 是不同的应用，它们的 session 存在自己的应用内，是不共享的

解决第一个问题: Cookie 的 domain 设置为顶域 example.com, 所以子域名都可以访问顶域的 Cookie. 这样 sit1, sit2 都带有 Cookies 了, 然后怎么共享 Session?  
解决第二个问题: sso, sit1, sit2 共用一个保存 Session 的数据库 redis

### 不同域的 SSO

1. 用户访问 sit1 系统, sit1 系统是需要登录的, 但用户现在没有登录
2. 跳转到 SSO 登录系统, SSO系统也没有登录, 弹出用户登录页
3. 用户填写用户名、密码, SSO系统进行认证后, 将登录状态写入 SSO 的 Session, 浏览器（Browser）中写入 SSO 域下的 Cookie
4. SSO系统登录完成后会生成一个ST (Service Ticket), 然后跳转到 sit1 系统, 同时将ST作为参数传递给 sit1 系统
5.  sit1 系统拿到ST后, 从后台向SSO发送请求, 验证ST是否有效
6. 验证通过后, sit1 系统将登录状态写入 Session 并设置 sit1 域下的 Cookie

sit2 系统同理


## 参考

> http://javascript.ruanyifeng.com/bom/cookie.html
> https://www.jianshu.com/p/75edcc05acfd?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation