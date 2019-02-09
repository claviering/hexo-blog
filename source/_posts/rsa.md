---
title: rsa
date: 2019-02-09 10:50:46
tags:
- cryptography
---
<script type="text/javascript" src='https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML' async></script>

# RSA

加密 \\(C \equiv M^e\ ( mod\ n ) \\)

解密 \\(M \equiv C^d\ ( mod\ n ) \\)

---

其中 n = pq (p, q是两个不同的大素数)

计算 t = \\( \phi(n)=(p-1)(q-1) \\)

选择 \\( 1<e<t \\), \\( e \in Z \\), 且 \\(gcd(e, t) = 1 \\)

公钥 (e, n), 私钥 (d, n)

## 安全性
1. 不同的用户不能用相同的模数 n
2. p 和 q 的差值要大，一般相差几个 bit
3. p-1 和 q-1 都应有大的素因子
4. 私钥 d 的选择，一般要求私钥 \\( d>=n^{0.25} \\)
5. 公钥 e 不可以太小
6. 如果 n 是模数，k 为任意正整数，m 是明文，那么 \\( e!=log_m(kn+m) \\), 否则密文和明文是一样的字符串
7. p-1 和 q-1 的最大公因子要小

## 破解

1. 对模数 n 的因子分解
2. 对 RSA 的公共模数攻击
    若一个多用户系统中只采用一个模数 n，不同的用户拥有不同的 e 和 d
3. 对 RSA 的小指数攻击
    e 取得太小
4. 对 RSA 的选择密文攻击
5. 时序攻击
## 参考

> [RSA 安全参数选择](https://www.jianshu.com/p/2d0183b62ca2)

> [简介对RSA算法的各种攻击](https://www.jianshu.com/p/76a05f18e969)

> [二十年以来对 RSA 密码系统攻击综述](https://paper.seebug.org/727/#5)