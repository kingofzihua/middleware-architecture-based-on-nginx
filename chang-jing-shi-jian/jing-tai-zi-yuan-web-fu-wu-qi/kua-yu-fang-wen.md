### 跨域访问
#### 为什么浏览器禁止跨域访问
不安全，容易出现CSRF攻击

#### nginx怎么设置
header头中有Access-Control-Allow-Origin属性，可以控制是否允许跨域请求

#### 配置语法
| header |  | 
| :-------- | :---- | :---- |
| 语法   | add_header name value [always] | 
| 默认   | --- | 
| 作用域 | http,server,location,if in location |

##### 例子:
```ngxin
    
    ...
    
    # 访问的所有以 htm或者 html结尾的
    location ~ .*\.(htm|html)$ {
        #设置 可以跨域访问的地址
        add_header Access-Control-Allow-Origin http://kingofzihua.com
        #设置 可以跨域的类型
        add_header Access-Control-Allow-Methods GET,POST,PUT,DELETE,OPTIONS;
        
        ...
        
    }
```