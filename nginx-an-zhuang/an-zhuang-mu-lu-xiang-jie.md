# 安装目录详解

| 路径 | 类型 | 作用 |
| :--- | :--- | :--- |
| /etc/logrotate.d/nginx | 配置文件 | Nginx日志轮转用于   logrotate服务日志的切割 |
| /etc/nginx   /etc/nginx/nginx.conf   /etc/nginx/conf.d   /etc/nginx/conf.d/default.conf | 目录、配置文件 | nginx住配置文件 |
| /etc/nginx/fastcgi\_params   /etc/nginx/uwsgi\_params   /etc/nginx/scgi\_params | 配置文件 | cgi配置相关,fastcgi配置 |
| /etc/nginx/koi-utf   /etc/nginx/koi-win   /etc/nginx/win-utf   | 配置文件 | 编码转换映射转化文件 |
| /etc/nginx/mime.types | 配置文件 | 设置http协议的Content-Type与扩展名对应关系 |
| /usr/lib/systemd/system/nginx-debug.service /usr/lib.systemd/system/nginx.service /etc/syconfig/nginx /etc/sysconfig/nginx-debug | 配置文件 | 用户配置出系统守护进程管理器管理方式 |
| /usr/lib64/nginx/modules   /etc/nginx/modules | 目录 | nginx模块目录 |
| /usr/sbin/nginx   /usr/sbin/nginx-debug | 命令 | nginx服务的启动管理的终端命令 |
| /usr/share/doc.nginx-1.12.0   /usr/share/doc/nginx-1.12.0/COPYRIGHT   /usr/share/man/man8/nginx.8.gz | 文件、目录 | nginx的手册和帮助文件 |
| /var/cache/nginx | 目录 | nginx的缓存目录 |
| /var/log/nginx | 目录 | nginx的日志目录 |

