---
title: Diffie-Hellman
date: 2019-02-11 11:36:11
tags:
- cryptography
---
<script type="text/javascript" src='https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML' async></script>

# Diffie-Hellman

Diffie-Hellman 密钥交换协议

## 描述

Alice:

1. 选择一个素数 `p`
2. 计算一个生成元 `g (mod p)`
3. 选择 `a` 作为私钥
4. 计算 \\( A = g^a\ (mod\ p) \\), 做为公钥
5. 发送 `p, g, A` 给 Bob

Bob:

1. 选择 `b` 作为私钥
2. 计算 计算 \\( B = g^b\ (mod\ p) \\), 做为公钥
3. 发送 `B` 给 Alice
4. 计算主密钥 \\( K = A^b\ (mod\ p) \\)

Alice:

1. 计算主密钥 \\( K = B^a\ (mod\ p) \\)

Alice, Bob 现在共享安全密钥 K

## 证明

\\( K_{Bob} = B^a\ (mod\ p) = (g^b)^a\ (mod\ p) = (g^a)^b\ (mod\ p) = A^b\ (mod\ p) = K_{Alice}\\)

## 安全性

存在中间人攻击

## 基于椭圆曲线的DH密钥交换 (ECDH)

Alice:

1. 选择一条椭圆曲线, 选择基点`P`
3. 选择 `a` 作为私钥
4. 计算 \\( A = aP \\), 做为公钥
5. 发送 椭圆曲线, `P, A` 给 Bob

Bob:

1. 选择 `b` 作为私钥
2. 计算 计算 \\( B = bP \\), 做为公钥
3. 发送 `B` 给 Alice
4. 计算主密钥 \\( K = Ab \\)

Alice:

1. 计算主密钥 \\( K = Ba \\)