### 调度算法

#### 算法详情
| 算法 | 详情 |
| --- |--- |
| 轮询 | 按时间顺序注意分配到不通的后端服务器 |
| 加权轮询 | weight值越大，分配到的访问几率越高 |
| ip_hash  | 每个请求按照访问IP的hash结果分配，这样来自同一个IP的固定访问一个后段服务器 |
| url_hash | 按照访问的URL的hash结果来分配请求，使每个URL定向到同一个后端服务器 |
| least_conn | 最少链接数,哪个及其连接数少就分发 |
| hash 关键数值 | hash 自定义的kay |

#### url_hash配置
| url_hash |  | 
| :-------- | :---- | :---- |
| 语法   | hash key [consistent] | 
| 默认   | --- | 
| 作用域 | upstream |
| 备注 | nginx version > 1.7.2 |

##### 例子:
```nginx

    ...
    
    # 在http里面
    upstream test{
        
        # 按照$request_uri进行hash 
        # $request_uri : /index?name=123 除域名以外的
        hash $request_uri;
        
        server 192.168.10.10:8001;
        server 192.168.10.10:8002;
        server 192.168.10.10:8003;
        
    }
    
    server {
        
        ...
        
        location / {
            # test是上面定义的upstream 的名字
            proxy_pass http://test
            proxy_redirect default; #302跳转的时候，默认
            
            ...
            
        }
        
        ...
    }
```