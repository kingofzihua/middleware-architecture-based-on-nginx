### Nginx 负载均衡
![](/assets/load-balancing-nginx.png)
#### 配置语法
| upstream |  | 
| :-------- | :---- | :---- |
| 语法   | upstream name {...} | 
| 默认   | --- | 
| 作用域 | http |

#### 后段服务器在负载调度中的状态
| 状态 | 介绍 |
| --- | --- |
| down | 当前的server暂时不参与负载均衡 |
| backup | 预留的备份服务器 |
| max_fails | 允许请求失败的次数 |
| fail_timeout | 经过max_fails失败后,服务暂停的时间 |
| max_conns | 限制最大的接受连接数 |

##### 例子:
```nginx
        ...
    # 在http里面
    upstream test{
        server 192.168.10.10:8001;
        
        # weight : 负载权重
        server 192.168.10.10:8002 weight=5;
        
        # backup : 表示这个是一个备份节点
        server 192.168.10.10:8003 backup; 
       
        # down : 表示这个节点不参与服务
        server 192.168.10.10:8004 down;
        
        # max_fails : 允许请求失败的次数 fail_timeout : 经过max_fails失败后,服务暂停的时间
        server 192.168.10.10:8005 max_fails=1 fail_timeout=10s;
        
        # unix : socket方式
        #server unix:/tmp/backend3; 
    }
    
    server {
        ....
        
        location / {
            # test是上面定义的upstream 的名字
            proxy_pass http://test
            proxy_redirect default; #302跳转的时候，默认
            
            ...
            
        }
        
        ...
    }
```