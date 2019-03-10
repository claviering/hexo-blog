---
title: opessl-crt
date: 2019-02-24 14:41:44
tags:
- openssl
---

# openssl 创建证书

RSA 和 ECC 的密钥生成不同，其他一样

## 配置文件

root.conf 根证书配置

```conf
[ req ]
default_bits       = 4096
default_md         = sha384
default_keyfile    = root.key
prompt             = no
# encrypt_key        = 123456
distinguished_name = req_distinguished_name
[ req_distinguished_name ]
countryName = "CN"
localityName = "GZ"
organizationName = "root"
organizationalUnitName = "root"
commonName = "root certificate"
emailAddress = "root@email.com"
```

server.conf 域名证书配置

```conf
[ req ]
default_bits       = 4096
default_md         = sha384
default_keyfile    = server.key
prompt             = no
distinguished_name = dn
[dn]
C = US
ST = localhostState
L = localhostCity
O = localhostOrganization
OU = localhostOrganizationUnit
emailAddress = localhost@email.address
CN = localhost
```

v3.ext 一证书多域名 配置

```conf
authorityKeyIdentifier = keyid,issuer
basicConstraints = CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[alt_names]
DNS.1 = localhost
DNS.2 = www.example.com
```



## 创建 RSA 证书

gen.sh

```bash
#!/bin/sh
# create self-signed server certificate:
source ~/.bashrc
echo 'make sure root.conf and server.conf file exist'
echo 'openssl version ...'
openssl version -a | echo
echo 'step 0: create root private key ...'
openssl genrsa -des3 -out root.key 2048
openssl req -x509 -new -config root.conf -key root.key -sha384 -days 3650 -out root.pem
echo 'step 1: create server csr'
openssl genrsa -out server.key 2048
openssl req -new -config server.conf -out server.csr
echo 'Remove passphrase from a key'
openssl rsa -in server.key -out server-without-passphrase.key
echo 'step 2: 用根证书颁发证书'
openssl x509 -req -in server.csr -CA root.pem -CAkey root.key -CAcreateserial -out server.crt -days 3650 -sha384 -extfile v3.ext
echo 'completed ...'
```
执行 `gen.sh` 自动生成

## 创建 ECC 证书

删除 root.conf 和 server.conf `default_bits       = 4096`

gen.sh

```bash
#! /bin/sh
# create self-signed server certificate:
echo 'make sure root.conf and server.conf file exist'
echo 'openssl version requset 1.1.1 ...'
echo 'step 0: create root private key ...'
openssl ecparam -name secp384r1 -genkey -out root.key
echo 'step 1: create root certificate ...'
openssl req -x509 -new -config root.conf -key root.key -sha384 -days 3650 -out root.crt
echo 'step 2: create server private key ...'
openssl ecparam -genkey -name secp384r1 -out server.key
echo 'step 3: create server csr ...'
openssl req -new -config server.conf -key server.key -out server.csr -sha384
echo 'step 4: 用根证书颁发证书'
openssl x509 -req -in server.csr -CA root.crt -CAkey root.key -CAcreateserial -out server.crt -days 3650 -sha384 -extfile v3.ext
echo 'completed ...'
```
执行 `gen.sh` 自动生成