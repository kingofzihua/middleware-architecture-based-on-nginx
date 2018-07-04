# HTTPS服务

HTTP不安全

* 传输数据被中间人盗用、信息泄露
* 数据内容被劫持、篡改

## HTTPS的实现

对传输内容进行加密以及身份验证

## 对称加密和非对称加密

对称加密 ![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/symmetric-encryption.png)

非对称加密 ![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/asymmetric-encryption.png)

## HTTPS加密协议原理

![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/https-encryption.png)

## 中间人伪造客户端和服务端

![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/client-forgery.png)

## HTTPS怎么防范中间人伪造

![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/keep-watch-client-forgery.png)

