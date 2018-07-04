# 代理缓存

![](https://github.com/kingofzihua/middleware-architecture-based-on-nginx/tree/2e7a10d6ee4bfe83fce6d75d27b818bc96a69f67/assets/proxy-cache.png)

## 配置语法

| proxy\_cache |  |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 语法 | proxy\_cache\_path path \[levels=levels\]   \[use\_temp\_path= on\|off\]   keys\_zone=name:size \[inactive=time\] \[max\_size=size\]   \[manager\_files=number\] \[manager\_sleep=time\]    \[manager\_threshold=time\]  \[loader\_files=number\]   \[loader\_sleep=time\] \[loader\_threshold=time\]   \[purger=on\|off\] \[purger\_files=number\]   \[purger\_sleep=time\] \[purger\_threshold=time\] | proxy\_cache zone\|off | proxy\_cache\_valid \[code ...\] time | proxy\_cache\_key sting |
| 默认 | --- | proxy\_cache off |  | proxy\_cache\_key   $scheme$proxy\_host$request\_uri |
| 作用域 | http | http,server,location | http,server,location | http,server,location |

### 例子:

```text
    ...

    upstream test{
        server 192.168.10.10:8001;
        server 192.168.10.10:8002;
        server 192.168.10.10:8003;
    }

    # /opt/app/cach : 缓存的目录 
    # levels : 按照两层目录来分级
    # keys_zone : imooc_cache代表开辟的空间名称 10m是开辟的空间大小 一般1m可以储存 8000个key
    # max_size : 最大空间是多少
    # inactive : 60分钟内 如果缓存没有命中 就会自动删除
    # use_temp_path : 用来存储临时文件的 关闭就好，开启的话 需要配置另一个目录
    proxy_cache_path /opt/app/cache levels=1:2 keys_zone=imooc_cache:10m max_size=10g inactive=60m use_temp_path=off;

    server {
        ...

        location / { 
            proxy_cache imooc_cache; # 上面配置的开辟的空间名称 
            proxy_pass http://test; # test 是上面定义的upstream名字 用来做负载
            proxy_cache_valid 200 304 12h; # 200 和304的信息缓存12小时
            proxy_cache_valid any 10m; # 其他的 10分钟过期
            proxy_cache_key $host$uri$is_args$args; # 定义缓存的key
            add_header Nginx-Cache "$upstream_cache_status"; # 添加一个header 告诉客户端是否命中

            # 反向代理服务用到 如果遇到错误，超时，不正确的头信息 跳过这一台 访问下一台
            proxy_next_upsteam error timeout invalid_header http_500 http_502 http_503 http_504;

            ...
        }

        ...
    }

    ...
```

