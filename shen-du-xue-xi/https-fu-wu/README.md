# HTTPS服务

HTTP不安全

* 传输数据被中间人盗用、信息泄露
* 数据内容被劫持、篡改

## HTTPS的实现

对传输内容进行加密以及身份验证

## 对称加密和非对称加密

对称加密 ![](https://kingofzihua.oss-cn-shanghai.aliyuncs.com/blog/nginx/symmetric-encryption.png)

非对称加密 ![](https://kingofzihua.oss-cn-shanghai.aliyuncs.com/blog/nginx/asymmetric-encryption.png)

## HTTPS加密协议原理

![](https://kingofzihua.oss-cn-shanghai.aliyuncs.com/blog/nginx/https-encryption.png)

## 中间人伪造客户端和服务端

![](https://kingofzihua.oss-cn-shanghai.aliyuncs.com/blog/nginx/client-forgery.png)

## HTTPS怎么防范中间人伪造

![](https://kingofzihua.oss-cn-shanghai.aliyuncs.com/blog/nginx/keep-watch-client-forgery.png)

