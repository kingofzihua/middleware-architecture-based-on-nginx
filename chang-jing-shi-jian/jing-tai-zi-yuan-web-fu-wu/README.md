# 静态资源web服务

## 静态资源服务

![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/static_resources_web_server.png)\#\#\# 静态资源服务

## 静态资源类型

| 类型 | 种类 |
| --- | --- |
| 浏览器端渲染 | HTML、CSS、JS |
| 图片 | JPEG、GIF、PNG |
| 视频 | FLV、MPEG |
| 文件 | TXT、等任意下载文件 |

## 静态资源服务场景-CDN

![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/static_resources_web_server_cdn.png)

## 配置语法

| 静态资源服务 |  |  |  |  |
| :--- | :--- | :--- | :--- |
| 语法 | sendfile on \| off | tcp\_nopush  on \| off | tcp\_nodelay on \| off |  |
| 默认 | sendfile off | tcp\_nopush off | tcp\_nopush on |  |
| 作用域 | http,server,location, if in location | http,server,location | http,server,location |  |
| 备注 |  | sendfile开启的情况下,提高网络包的传输效率 | keepalive连接下,提高网络包的传输实时行 |  |

