# 大文件分片请求

## 图示

![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/http_slice_module.png)

## 配置语法

| slice |  |
| :--- | :--- | :--- |
| 语法 | slice size |
| 默认 | slice 0 |
| 作用域 | http,server,location |
| 备注 |  |

### 优势

每个自请求收到的数据都会形成一个独立文件，一个请求断了，其他请求不受影响

### 缺点

当文件很大或者slice很小的时候,可能会导致文件描述符耗尽等情况

