+++
categories = ["java"]
date = "2015-01-09T00:00:00+08:00"
description = ""
keywords = ["Build","CMS","Gulp","Maven","Gradle","CD"]
title = "HttpClient Ultimate Document"
draft = true

+++

Apache HttpClient，在工作中经常使用，可用起来并不完全那样，尤其是对于初学者。

## Quick Start
首先，从fluent-hc开始，
```java
URI uri = new URIBuilder("http://www.baidu.com/s").addParameter("wd",
    "simple is not easy").build();

String entity = Request.Get(uri).connectTimeout(1000)
    .socketTimeout(1000).execute().returnContent().asString();

assertThat(entity, new StringContains("simple"));
```
简单来看，的确是对Request/Response的处理，

## HttpMessage

## HttpRequest

## HttpResponse



## HttpClient

## HTTPS
Cipher 将cleartext/plaintest 转换成ciphertext

Keyed Cipers  key是码的位移量

Digital Key，very large keys

对称秘钥算法 导致双方维护秘钥2^n个秘钥对
非对称秘钥，用public key encoding，private key decoding

Hybrid Cryptosystems 非对称connection，对称临时短暂的交流，满足效率。

Digital Signatures  private key checksum

Digital Certificates id card

Proxy method connect to forword

## Tips



## Reference
http://hc.apache.org/httpcomponents-core-4.4.x/tutorial/html/index.html[HttpCore Tutorial]

http://hc.apache.org/httpcomponents-client-4.4.x/tutorial/html/index.html[HttpClient Tutorial]

https://tools.ietf.org/html/rfc7230[Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing]

https://tools.ietf.org/html/rfc7231[Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content]
