### 代理服务

![](/assets/proxy-chart.png)
![](/assets/proxy-chart-1.png)
#### 正向代理
正向代理代理的对象是客户端
![](/assets/forward-agent.png)
#### 反向代理
反向代理代理的对象是服务端
![](/assets/reverse-proxy.png)

#### 配置语法
| proxy |  | 缓冲区 | 跳转重定向 | 头信息 | 超时 |
| :-------- | :---- | :---- | :---- | :---- | :---- |
| 语法   | proxy_pass URL | proxy_buffering on \| off  | proxy_redirect default \| off \| redirect replacement | proxy_set_header field value | proxy_connect_timeout time |
| 默认   | --- | proxy_buffering on | proxy_redirect default| proxy_set_header Host $proxy_host <br /> proxy_set_header Connection close | proxy_connect_timeout 60s |
| 作用域 | location,if in location, limit_except | http,server,location | http,server,location | http,server,location | http,server,location |
| 扩展 |  | proxy_buff_size <br /> proxy_buffers <br /> proxy_busy_buffers_size |  | proxy_hide_header <br /> proxy_set_boby | proxy_read_timeout <br /> proxy_send_timeout |
| 备注 |  |  | 代理的时候如果是302重定向了需要这个 |  |

##### 例子:
```ngixn
    # 反向代理
    ...
    
    # 匹配 proxy 访问 转发给 8080端口
    location ~ /proxy$ {
        proxy_pass http://127.0.0.1:8080
    }
```

```ngixn
    # 正向代理
    ...
    
    # 匹配 proxy 访问 转发给 8080端口
    resolver 8.8.8.8 #设置dns服务器
    
    #将所有访问转发
    location / {
        proxy_pass http://$http_host$request_uri;
    }
```

```ngixn
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