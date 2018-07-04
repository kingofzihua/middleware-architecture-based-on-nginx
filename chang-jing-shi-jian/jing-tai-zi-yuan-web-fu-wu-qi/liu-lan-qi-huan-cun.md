### 浏览器缓存
HTTP协议定义的缓存机制(如:Expires; Cache-control 等)

#### 请求机制
##### 浏览器无缓存时
![](/assets/browser-cache-no.png)

##### 浏览器有缓存时
![](/assets/browser-cache-has.png)

##### 校检过期机制
| 校检是否过期 | Expires、Cache-Control(max-age) |
| --- | --- |
| 协议中Etag头信息校检 | Etag |
| Last-Modified头信息校检 | Last-Modified |

###### Expires: http 1.0里面     Cache-Control: http 1.1里面

##### 浏览器缓存原理
![](/assets/861554-20160820111456437-1615310660.png)

#### 配置语法
| expires |  | 
| :-------- | :---- | :---- |
| 语法   | expires [modified] time <br /> expires epoch \|max \| off | 
| 默认   | expires off | 
| 作用域 | http,server,location,if in location |

##### 例子:

```ngxin
    
    ...
    
    # 访问的所有以 htm或者 html结尾的
    location ~ .*\.(htm|html)$ {
        expires 24h; # 缓存24小时
        
        ...
        
    }
```
###### 对于不同的浏览器 他们会有默认的请求方式，可能会自动缓存，也可能会覆盖掉你设置的缓存！

