# 常见问题

## 相同server\_name多个虚拟主机优先级访问

### 伪代码

```text
    server{
        listen 80;
        server_name test_server_1 name.kingofzihua.top;
        location {
            ...
        }
    }

    server{
        listen 80;
        server_name test_server_2 name.kingofzihua.top;
        location {
            ...
        }
    }
```

查找的时候按照你系统文件加载的第一个,一般来说 a.conf &gt; b.conf,并且如果直接访问ip,但是你的server name 并没有配置，则会访问你配置的第一个虚拟域名。

## location 匹配优先级

### 配置语法

| location |  |
| :--- | --- |
| = | 进行普通字符精确匹配,也就是完全匹配 |
| ^~ | 表示普通字符匹配,使用前缀匹配 |
| ~ ~\* | 表示执行一个正则匹配 |

## try\_files 的使用

按照顺序检查文件是否存在

### 例子:

```text
    # laravel 配置
    location / {
        # 首先检查$url是否存在,然后检查是否是一个目录,如果也不是就交给inde.php来处理
        try_files $url $url/ /index.php/?$query_string
    }
```

## alias和root 区别

### 例子:

```text
    location /root {
        #  实际路径为/local_path/image/root
        root /local_path/image;
    }

    location /alias {
        #  实际路径为/local_path/image
        alias /local_path/image;
    }
```

## 传递用户的真实IP地址

自定义一个header 头 用来传递用户的信息 ![](https://kingofzihua.oss-cn-shanghai.aliyuncs.com/blog/nginx/x_real_ip.png)

