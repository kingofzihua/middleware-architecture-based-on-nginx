# 代理服务

![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/proxy-chart.png) ![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/proxy-chart-1.png)

## 正向代理

正向代理代理的对象是客户端 ![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/forward-agent.png)

## 反向代理

反向代理代理的对象是服务端 ![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/reverse-proxy.png)

## 配置语法

| proxy |  | 缓冲区 | 跳转重定向 | 头信息 | 超时 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 语法 | proxy\_pass URL | proxy\_buffering on \| off | proxy\_redirect default \| off \| redirect replacement | proxy\_set\_header field value | proxy\_connect\_timeout time |
| 默认 | --- | proxy\_buffering on | proxy\_redirect default | proxy\_set\_header Host $proxy\_host   proxy\_set\_header Connection close | proxy\_connect\_timeout 60s |
| 作用域 | location,if in location, limit\_except | http,server,location | http,server,location | http,server,location | http,server,location |
| 扩展 |  | proxy\_buff\_size   proxy\_buffers   proxy\_busy\_buffers\_size |  | proxy\_hide\_header   proxy\_set\_boby | proxy\_read\_timeout   proxy\_send\_timeout |
| 备注 |  |  | 代理的时候如果是302重定向了需要这个 |  |  |

### 例子:

```text
    # 反向代理
    ...

    # 匹配 proxy 访问 转发给 8080端口
    location ~ /proxy$ {
        proxy_pass http://127.0.0.1:8080
    }
```

```text
    # 正向代理
    ...

    # 匹配 proxy 访问 转发给 8080端口
    resolver 8.8.8.8 #设置dns服务器

    #将所有访问转发
    location / {
        proxy_pass http://$http_host$request_uri;
    }
```

```text
    # 常用代理的配置方式 demo

    ...

    location / {
        proxy_pass http://127.0.0.1:8080
        proxy_redirect default; //302跳转的时候，默认

        proxy_set_header Host $http_host
        proxy_set_header X-Real-IP $remote_addr; //真实的ip信息要返回给后面

        proxy_connect_timeout 30;
        proxy_send_timeout 60;
        proxy_read_timeout 60;

        proxy_buffer_size 32k; # 缓冲区大小
        proxy_buffering on; 
        proxy_buffers 4 128k;
        proxy_busy_buffers_size 256k;
        proxy_max_temp_file_size 256k; # 临时文件大小
    }

    ...
```

