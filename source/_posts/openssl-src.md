---
title: openssl-src
date: 2019-02-09 14:36:55
tags:
- openssl
---

# openssl 源代码分析

[Github](https://github.com/openssl/openssl)

openssl整个软件包主要包括三个主要的功能模块

1. 密码算法库
2. SSL/TLS协议库
3. 应用程序
   1. 密钥生成
   2. 证书管理
   3. 格式转换
   4. 数据加密
   5. 签名
   6. SSL/TLS测试等

## 目录结构

                        
    openssl
    ├── apps 应用程序
    ├── Configurations 配置
    ├── crypto 密码算法库
    |  ├── asn.1 DER编码解码
    |  ├── bio 包含各种输入输出抽象，文件、内存、stdio、socket、SSL
    |  ├── bn 大数运算
    |  ├── buffer 字符缓存
    |  ├── conf 配置文件读取, 主要配置文件为openssl.cnf
    |  ├── engine 硬件引擎, 提供了规定接口
    |  ├── err 错误处理, 提供处理接口；以堆栈显示错误
    |  ├── evp 对称算法、非对称算法及摘要算法封装
    |  ├── hmac 实现基于对称算法的MAC
    |  ├── lhash 实现散列表数据结构
    |  ├── ocsp OCSP数字证书在线认证, 实现ocsp协议的编解码等
    |  ├── pem 生成和读取PEM文件
    |  ├── pkcs7 实现构造和解析PKCS7消息
    |  ├── pkcs12 实现pkcs12证书构造和解析
    |  ├── pqueue 实现队列数据结构, 用于DTLS
    |  ├── rand 实现伪随机数生成
    |  ├── stack 实现堆栈数据结构
    |  ├── threads openssl支持多线程, 但是用户必须实现相关接口
    |  ├── txt_db 文本数据库
    |  └── x509 包括数字证书申请、证书和CRL构造解析和签名验证
    ├── demos 示例
    ├── doc 文档
    ├── engines 引擎
    ├── external 拓展
    ├── ssl SSL/TLS协议库
    └── test 测试使用
                        

## 参考

[Openssl源代码整理学习](https://www.cnblogs.com/testlife007/p/6699566.html)