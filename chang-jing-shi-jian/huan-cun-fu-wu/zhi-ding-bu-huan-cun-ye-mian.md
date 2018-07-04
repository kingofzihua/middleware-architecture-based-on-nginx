# 指定不缓存页面

## 配置语法

| proxy\_no\_cache |  |
| :--- | :--- | :--- |
| 语法 | proxy\_no\_cache string ... |
| 默认 | --- |
| 作用域 | http,server,location |
| 备注 |  |

### 例子:

```text
    ...

    # 判断当前路径是否是指定的路径
    if($request_uri ~ ^/(url3|login|register|password\/reset)) {
        设置一个变量用来存储是否是需要缓存
        set $cookie_nocache 1;
    }

    location / {
        ...

        proxy_no_cache $cookie $arg_nocache $arg_comment;

        ...
    }

    ...
```

