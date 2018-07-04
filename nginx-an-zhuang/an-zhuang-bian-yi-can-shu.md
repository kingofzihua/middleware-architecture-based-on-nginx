# 安装编译参数

## 查看安装编译参数

```text
   # 查看安装编译参数
   nginx -V
```

## 编译选项

| 编译选项 | 作用 |
| :--- | :--- |
| --prefix=/etc/nginx   --sbin-path=/usr/sbin/nginx/modules   --modules-path=/usr/lib64/nginx/models   --config-path=/etc/nginx/nginx.conf   --error-log-path=/var/log/nginx/error.log   --http-log-path=/var/log/nginx/access.log   --pid-path=/var/run/nginx.pid   --lock-path=/var/run/nginx.lock | 安装目的目录或路径 |
| --http-client-boby-temp-path=/var/cache/nginx/client\_temp   --http-proxy-temp-path=/var/cache/nginx/proxy\_temp   --http-fastcgi-temp-path=/var/cache/nginx/uwsgi\_temp   --http-scgi-temp-path=/var/cache/nginx/scgi\_temp | 执行对应模块是,nginx所保留的临时性的文件 |
| --user=nginx   --gtoup=nginx | 设定nginx进程启动的用户和用户组 |
| --with-cc-opt=parameters | 设置额外的参数将被添加到CFLAGS变量 |
| --with-ld-opt=parameters | 设置附加的参数,链接系统库 |
| --with-http\_stub\_status\_module | nginx的客户端状态 |
| --with-http\_random\_index\_module | 目录中选择一个随机主页 |
| --with-http\_sub\_module | http内容替换 |
| --with-http\_gzip\_static\_module | 预读gzip功能 |
| --with-http\_gunzip\_module | 应用支持gunzip的压缩方式\(部分浏览器不支持gzip \) |
| --with-http\_gunzip\_module | 大文件分片请求 |

