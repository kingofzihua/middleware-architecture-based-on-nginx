# secure\_link\_module 模块

* 制定并允许检查请求的链接的真实性以及保护资源免遭未经授权的访问
* 限制链接生效周期

  **图示**

  下载:

  ![](https://kingofzihua.oss-cn-shanghai.aliyuncs.com/blog/nginx/secure_link_module_download.png)

验证: ![](https://kingofzihua.oss-cn-shanghai.aliyuncs.com/blog/nginx/secure_link_module_validate.png)

## 配置语法

| secure\_link\_module |  |  |
| :--- | :--- | :--- | :--- |
| 语法 | secure\_link expression | secure\_link\_md5 expression |
| 默认 | --- |  |
| 作用域 | server,location | http,server,location |
| 例如 |  |  |

### 例子:

```text
    ...

    location / {
        # $arg_md5 : 从参数中取得md5 (url get )
        # $arg_expires :  从参数中取得expires
        secure_link $arg_md5,$arg_expires;
        # 进行md5加密 "这里面是加密的字符串" 将过期时间和字符串拼接上imooc来做加密字符串
        secure_link_md5 "$secure_link_expires$url imooc";

        if ($secure_link = "") {
            return 403;
        }

        if ($secure_link = "0") {
            return 410;
        }
    }

    ...
```

