### 安装编译参数

#### 查看安装编译参数

```shell
   # 查看安装编译参数
   nginx -V
```
#### 编译选项

| 编译选项  | 作用  |
| :-------- | :---- |
| --prefix=/etc/nginx <br /> --sbin-path=/usr/sbin/nginx/modules <br /> --modules-path=/usr/lib64/nginx/models <br /> --config-path=/etc/nginx/nginx.conf <br /> --error-log-path=/var/log/nginx/error.log <br /> --http-log-path=/var/log/nginx/access.log <br /> --pid-path=/var/run/nginx.pid <br /> --lock-path=/var/run/nginx.lock | 安装目的目录或路径 |
| --http-client-boby-temp-path=/var/cache/nginx/client_temp <br /> --http-proxy-temp-path=/var/cache/nginx/proxy_temp <br /> --http-fastcgi-temp-path=/var/cache/nginx/uwsgi_temp <br /> --http-scgi-temp-path=/var/cache/nginx/scgi_temp | 执行对应模块是,nginx所保留的临时性的文件 |
| --user=nginx <br /> --gtoup=nginx | 设定nginx进程启动的用户和用户组 |
| --with-cc-opt=parameters | 设置额外的参数将被添加到CFLAGS变量 |
| --with-ld-opt=parameters | 设置附加的参数,链接系统库 |
| --with-http_stub_status_module | nginx的客户端状态 |
| --with-http_random_index_module | 目录中选择一个随机主页 |
| --with-http_sub_module | http内容替换 |
| --with-http_gzip_static_module | 预读gzip功能 |
| --with-http_gunzip_module | 应用支持gunzip的压缩方式(部分浏览器不支持gzip ) |
| --with-http_gunzip_module | 大文件分片请求 |