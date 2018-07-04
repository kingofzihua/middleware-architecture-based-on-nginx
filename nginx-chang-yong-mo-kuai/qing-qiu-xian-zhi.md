### 连接限制

#### 配置语法
| limit_conn |  |   |
| :-------- | :---- | :---- |
| 语法   | limit_conn_zone key zone=name:size | limit_conn zone number |
| 默认   | --- | --- | 
| 作用域 | http | http,server,location | 
| 备注 | name: 定义的名字 size:定义的空间大小   |  |

##### 例子:
```nginx
    # 注意 应该在http里面 server 外面 
    # $binanry_remote_addr 和$remote_addr 一样 但是 减少空间
    limit_conn_zone $binanry_remote_addr zone=conn_zone:1m
    
    server{
        ...
        
        location / {
            # 同一时段 只有1个IP能访问
            limit_conn conn_zone 1;
        }
    }

```

### 请求限制
#### 配置语法
| limit_req |  |  |
| :-------- | :---- | :---- | 
| 语法   | limit_req_zone key zone=name:size rate=rate | limit_req zone=name [ burst=number ]  [ nodelay ] |
| 默认   | --- | --- |
| 作用域 | http | server,location |
| 备注 | name: 定义的名字 size:定义的空间大小 rate:速率【一般来说是每秒多少个】  |  |

##### 例子:

```nginx
    # 注意 应该在http里面 server 外面 
    # $binanry_remote_addr 和$remote_addr 一样 但是 减少空间
    # rate:【1r/s:每秒一个】
    limit_req_zone $binanry_remote_addr zone=req_zone:1m rate=1r/s 
    
    server{
        ...
        
        location / {
            # 当超过限制的时候，我最多允许3个再进行处理，剩下的失败
            limit_req zone=req_zone burst=3 nodelay;
        }
    }
```