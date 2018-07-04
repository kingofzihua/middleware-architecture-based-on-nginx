# 动静分离

通过中间件将动态请求和静态请求分离

## 为什么？

分离资源，减少不必要的请求消耗，减少请求延时

## 原理

静态资源直接返回，不需要后端服务进行处理 ![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/static-and-dynamic-separation.png)

## 场景

请求静态资源nginx直接返回，动态资源资源tomcat ![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/static-and-dynamic-separation-demo.png)

