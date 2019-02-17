---
title: key-exchange
date: 2019-02-17 11:26:33
tags:
- cryptography
---

# TLS 中的密钥交换

使用非对称加密算法密钥交换

## RSA

    Client                                               Server
    
    申请 RSA 密钥交换              -------->
                                 <--------             证书(公钥)
    生成主密钥 K, 公钥加密 E
    发送 E                        --------> 
                                                    私钥解密得到 K
    

双方共享密钥 K，私钥泄露，解密得到 K，从而解密报文，不具有前向安全性

## DHE

    
    Client                                               Server
    
    申请 DHE 密钥交换              -------->
                                                 DHE 参数 p, g, a
                                    计算 A = g^a (mod p), 做为公钥
                                 <--------           发送 p, g, A
    选择 b 作为私钥
    计算 B = g^b (mod p), 做为公钥
    计算主密钥 K = A^b (mod p)
    发送 B                        --------> 
                                         计算主密钥 K = B^a (mod p)
    

双方共享密钥 K，因为 Client， Server 私钥的临时生成的， 不依赖 Server 私钥，即使 Server 私钥泄露，也解密不出 K，具有前向安全性

## ECDHE

    
    Client                                               Server
    
    申请 ECDHE 密钥交换              -------->
                                ECDHE 参数: 选择曲线, 私钥 a, 基点 G
                                              计算 A = aG, 做为公钥
                                 <--------         发送 曲线, G, A
    选择 b 作为私钥
    计算 B = bG, 做为公钥
    计算主密钥 K = bA = abG
    发送 B                        --------> 
                                             计算主密钥 K = aB = abG
    

双方共享密钥 K，因为 Client， Server 私钥的临时生成的， 不依赖 Server 私钥，即使 Server 私钥泄露，也解密不出 K，具有前向安全性

## ECDHE 与 ECDH 算法的区别

字面少了一个E，E代表了 临时(extempore)，即在握手流程中，作为服务器端，ECDH 少了一步计算公钥的过程，直接使用证书中的公钥。使用ECDH密钥交换算法，服务器必须采用ECC证书；服务器不发送 server key exchange 报文，因为发送 certificate 报文时，证书本身就包含了公钥信息。

## ECDHE 与 RSA 的区别

ECDHE 算法属于 DH 类密钥交换算法， 私钥不参与密钥的协商，故即使私钥泄漏，客户端和服务器之间加密的报文都无法被解密，这叫前向安全（forward secrity）。由于 ECDHE 每次会话都重新计算一个密钥，故一条会话被解密后，其他会话仍旧安全。

然而，ECDH 算法服务器端的私钥是固定的，证书作为公钥，故 ECDH 不被认为前向安全，因为私钥泄漏导致会话密钥可被第三方计算

## 参数

> [TLS/SSL 协议详解 (30) SSL中的RSA、DHE、ECDHE、ECDH流程与区别](https://blog.csdn.net/mrpre/article/details/78025940)