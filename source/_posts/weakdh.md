---
title: weakdh
date: 2019-02-11 11:30:11
tags:
- security
---

## 弱 Diffie-Hellman 和 Logjam(堵塞) 攻击

Diffie-Hellman密钥交换是一种流行的加密算法，它允许Internet协议就共享密钥达成一致并协商安全连接。 它是许多协议的基础，包括HTTPS，SSH，IPsec，SMTPS和依赖于TLS的协议。

我们已经发现了如何部署Diffie-Hellman密钥交换的几个弱点：

1. 针对TLS协议的Logjam攻击。 Logjam攻击允许中间人攻击者将易受攻击的TLS连接降级为512位出口级加密。 这允许攻击者读取和修改通过连接传递的任何数据。 这次攻击让人想起FREAK攻击，但是由于TLS协议存在缺陷而不是实施漏洞，并且攻击Diffie-Hellman密钥交换而不是RSA密钥交换。 攻击会影响支持DHE_EXPORT密码的任何服务器，并影响所有现代Web浏览器。 前100万个域名中有8.4％是脆弱的。
2. 来自州级对手的威胁。 数以百万计的HTTPS，SSH和VPN服务器都使用相同的素数进行Diffie-Hellman密钥交换。 只要为每个连接生成新的密钥交换消息，从业者就认为这是安全的。 然而，数字域筛选的第一步 - 打破Diffie-Hellman连接的最有效算法 - 仅取决于该素数。 在第一步之后，攻击者可以快速破坏个人连接。

我们针对用于TLS的最常见的512位素数执行此计算，并证明Logjam攻击可用于将连接降级到支持DHE_EXPORT的80％的TLS服务器。 我们进一步估计，一个学术团队可以打破一个768位的素数，一个国家可以打破一个1024位的素数。 打破Web服务器使用的单个最常见的1024位素数将允许对18％的前1百万个HTTPS域的连接进行被动窃听。 第二个素数将允许被动解密连接到66％的VPN服务器和26％的SSH服务器。 仔细阅读已公布的国家安全局泄密事件表明，该机构对VPN的攻击与实现这种突破是一致的。

## 完整的技术论文

> [Imperfect Forward Secrecy: How Diffie-Hellman Fails in Practice](https://weakdh.org/imperfect-forward-secrecy-ccs15.pdf)

## 附加信息

> [为TLS部署Diffie-Hellman](https://weakdh.org/sysadmin.html)

> [概念演示证明](https://weakdh.org/logjam.html)