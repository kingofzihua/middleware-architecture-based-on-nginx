# 访问控制\(http\_access\_module\)

## 基于ip的访问控制

只能通过$remote\_addr控制信任,如果有代理的话就没法确认了

### 配置语法

| http\_access\_module | 允许 | 不允许 |
| :--- | :--- | :--- |
| 语法 | allow address \| CIDR \| unix: \| all | deny address \| CIDR \| unix: \| all |
| 默认 | --- | --- |
| 作用域 | http,server,location,limit\_except | http,server,location,limit\_except |
| 备注 | address:ip CIDR:网段 unix:socket方式访问 all:所有 | 同左 |

#### 例子:

```text
   location ~ ^/admin {
       root /www/nginx/access/
       allow 1.198.210.118; #限制 1.198.210.118 ip 能访问
       deny all; # 禁止所有人访问
   }

   location ~ ^/index {
       root /www/nginx/access/
       deny 1.198.210.118; #限制 1.198.210.118 ip 不能访问
       allow all; # 允许所有人访问
   }
```

## 基于用户的信任登录

### 配置语法

| http\_auth\_basic\_module |  |  |
| :--- | :--- | :--- |
| 语法 | auth\_basic string \| off | auth\_basic\_user\_file file |
| 默认 | auth\_basic off | --- |
| 作用域 | http,server,location,limit\_except | http,server,location,limit\_except |
| 备注 |  |  |

#### 例子:

```text
   # 确保自己服务器上有htpasswd 没有的话安装下 httpd-tools
   #centOS
   yum install httpd-tools -y

   返回上级目录，将密码文件放到 /etc/nginx 下
   cd ../

   #生成 加密密码 ./auth_conf : 生成的密码文件 kingofzihua : 用户名 -c : 创建
   # 如果是第一次执行的话 用-c 表示创建 以后的话会覆盖，如果要追加 去掉 -c 
   htpasswd -c ./auth_conf kingofzihua 
   #输入密码
   #确认密码

   cat ./auth_conf
   kingofzihua:$apr1$avun6caa$P6Te4xLkFQTEuVXKC4CPF1
   #查看密码

   nginx
   #打开nginx配置文件 修改
   # 匹配 /admin 路径
   location ~ ^/admin {
       ...
       auth_basic "Auth: input your passward!";
       auth_basic_user_file /etc/nginx/auth_conf; #设置密码储存的文件
   }
```

