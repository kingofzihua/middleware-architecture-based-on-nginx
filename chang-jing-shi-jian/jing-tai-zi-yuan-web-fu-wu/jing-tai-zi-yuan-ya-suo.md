# 静态资源压缩

![](https://kingofzihua.oss-cn-shanghai.aliyuncs.com/blog/nginx/static_resources_web_server_gzip.png)

## 配置语法

| gzip压缩 |  |  |  |
| :--- | :--- | :--- | :--- |
| 语法 | gzip on \| off | gzip\_comp\_level level | gzip\_http\_version 1.0 \| 1.1 |
| 默认 | gzip off | gzip\_comp\_level 1 | gzip\_http\_version 1.1 |
| 作用域 |  | http,server,location | http,server,location |
| 备注 | 是否开启 | gzip压缩级别 | gzip版本 |

### 例子:

```text
   server{
       sendfile on;

       ...

       #图片 压缩等级2
       location ~ .*\.(jpg|gif|png)$ {
           gzip on;
           gzip_http_version 1.1;
           gzip_comp_level 2; 
           gzip_types text/plain application/javascript application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png
       }

       #文本 压缩等级1
       location ~ .*\.(txt|xml)$ {
           gzip on;
           gzip_http_version 1.1;
           gzip_comp_level 1; 
           gzip_types text/plain application/javascript application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png
       }

       #以/download开头的路径为下载文件
       location ~ ^/download {
           #gzip_static 开启是为了不让请求时 nginx 进行实时的压缩，减少cpu的损耗
           gzip_static on; #gzip 预读功能 我事先压缩好 到时候直接返回
           tcp_nopush on;
           gzip_comp_level 1; 
       }
       #gzip 预读功能 要使用的时候要在服务器上先压缩 比如要访问 /download/test.img 如果gzip_static 为on 则 文件实际为 test.img.gz 

   }
```

