### 防盗链
#### 目的
防止资源被盗用
#### 基于http_refer防盗链配置模块
http_refer会储存发起请求的地址是什么 当从标签栏或者是地址栏进入的时候为空
##### 配置语法
| referers |  | 
| :-------- | :---- | :---- |
| 语法   | valid_referers none \| blocked \|server_names \| string ... | 
| 默认   | --- | 
| 作用域 | server,location |
##### 例子:
```nginx

    localhost ~ .*\.(jpg|gif|png)$ {
        
        ...
        
        #允许那些人可以访问 
        #none: 没有带refer的 |
        #blocked : refer信息不是标准的http协议的 
        #1.198.216.118 : 只允许1.198.216.118 ip访问
        #~/google\./ : 所有以google.的域名都可以访问
        valid_referers none blocked 1.198.216.118 ~/google\./;
        
        if($invalid_referer) {
            return 403
        }
        
        ...
        
    }

```