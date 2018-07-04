# Nginx配置语法

## 默认配置语法

### root

| 配置组 | 配置项 | 作用 | 备注 |
| :--- | :--- | :--- | :--- |
| root | user | 设置nginx服务的系统使用用户 |  |
|  | worker\_processes | 工作进程数 | 一般和cpu保持一致 |
|  | error\_log | nginx错误日志 |  |
|  | pid | nginx服务启动时候pid |  |

### events

| 配置组 | 配置项 | 作用 | 备注 |
| :--- | :--- | :--- | :--- |
| events | worker\_connectionss | 每个进程允许最大连接数 |  |
|  | use | 工作进程数 |  |

### http

| 配置组 | 配置项 | 作用 | 备注 |
| :--- | :--- | :--- | :--- |
| http | default\_type | 默认返回的类型 | 指的是返回的 Content-Type |
|  | log\_format | 记录日志的格式 |  |
|  | access\_log | 成功的日志 |  |
|  | sendfile | 是否开启`sendfile` |  |
|  | keepalive\_timeout | 长连接时间 |  |
|  | gzip | 是否开启gzip压缩 |  |
|  | include | 引入文件 |  |

### server

| 配置组 | 配置项 | 作用 | 备注 |
| :--- | :--- | :--- | :--- |
| server | listen | 监听的端口 | `80`:http `443`:https |
|  | server\_name | 域名 | `localhost`:本地 `127.0.0.1`:本机 `www.baidu.com`:外部域名 |
|  | root | 定义根路径 | 一般指程序的根目录 |
|  | index | 定义默认访问的文件 | nginx会按照 指定的顺序查找相对应的文件 |
|  | error\_page | 错误页面 | `404` `500` `502` 错误码及其页面所在地址.    **例如:** `error_page  404   /404.html`; |
|  | location | 匹配路径 | 用于匹配指定的路径或者文件 |
|  | ssl | 是否开启ssl |  |
|  | ssl\_certificate | ssl证书 |  |
|  | ssl\_certificate\_key | ssl证书 |  |
|  | ssl\_dhparam | ssl证书 |  |

