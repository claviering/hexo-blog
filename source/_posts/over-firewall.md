---
title: over-firewall
date: 2019-02-02 17:40:57
tags:
- TLS
- firewall
---

# 利用SSL/TLS绕过Web应用防火墙

原理: 选择防火墙不支持的加密套件, 但是服务器支持的加密套件

## 防火墙支持的加密方式
通过查阅了WAF厂商的文档，从中找到了所有受支持的SSL加密方式
## 服务器支持的加密方式
检查工具 `sslscan`

[Github](https://github.com/rbsec/sslscan)

使用 `sslscan https://target/ | grep Accept`

## 测试绕过

`curl --ciphers ECDHE-RSA-AES256-SHA https://target`

## 参考

[利用SSL/TLS绕过Web应用防火墙(实用技巧)](https://www.wosign.com/news/news_2019010201.htm)