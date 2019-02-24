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
default_keyfile    = private.key
prompt             = no
# encrypt_key        = 123456
distinguished_name = req_distinguished_name
[ req_distinguished_name ]
countryName = "CN"
localityName = "GZ"
organizationName = "weiye"
organizationalUnitName = "weiye"
commonName = "localhost certificate"
emailAddress = "weiye@mail.com"
```

domain.conf 域名证书配置

```conf
[ req ]
default_bits       = 4096
default_md         = sha384
default_keyfile    = domain.key
prompt             = no
distinguished_name = dn
[dn]
C = US
ST = weiyeState
L = weiyeCity
O = weiyeOrganization
OU = weiyeOrganizationUnit
emailAddress = weiye@email.address
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
DNS.3 = 127.0.0.1
DNS.2 = www.example.com
```



## 创建 RSA 证书

gen.sh

```bash
#!/bin/sh
# create self-signed domain certificate:
source ~/.bashrc
echo 'make sure root.conf and domain.conf file exist'
echo 'openssl version ...'
openssl version -a | echo
echo 'step 0: create root private key ...'
openssl genrsa -des3 -out root.key 2048
openssl req -x509 -new -config root.conf -key root.key -sha384 -days 3650 -out root.pem
echo 'step 1: create domain csr'
openssl genrsa -out domain.key 2048
openssl req -new -config domain.conf -out domain.csr
echo 'Remove passphrase from a key'
openssl ecparam -in domain.key -out domain-without-passphrase.key
echo 'step 2: 用根证书颁发证书'
openssl x509 -req -in domain.csr -CA root.pem -CAkey root.key -CAcreateserial -out domain.crt -days 3650 -sha384 -extfile v3.ext
echo 'completed ...'
```
执行 `gen.sh` 自动生成

## 创建 ECC 证书

gen.sh

```bash
#!/bin/sh
# create self-signed domain certificate:
source ~/.bashrc
echo 'make sure root.conf and domain.conf file exist'
echo 'openssl version ...'
openssl version -a | echo
echo 'step 0: create root private key ...'
openssl ecparam  -genkey -out root.key
openssl req -x509 -new -config root.conf -key root.key -sha384 -days 3650 -out root.pem
echo 'step 1: create domain csr'
openssl ecparam  -genkey -out domain.key
openssl req -new -config domain.conf -out domain.csr
echo 'Remove passphrase from a key'
openssl ecparam -in domain.key -out domain-without-passphrase.key
echo 'step 2: 用根证书颁发证书'
openssl x509 -req -in domain.csr -CA root.pem -CAkey root.key -CAcreateserial -out domain.crt -days 3650 -sha384 -extfile v3.ext
echo 'completed ...'
```
执行 `gen.sh` 自动生成