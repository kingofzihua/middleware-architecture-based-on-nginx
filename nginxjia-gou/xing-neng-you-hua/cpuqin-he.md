### CPU亲和
#### 查看当前机器cpu
```shell
    # 查看当前机器物理cpu数量
    cat /proc/cpuinfo|grep "physical id"|sort|uniq|wc -l
    # 1
    
    # 查看当前机器物理cpu核心数量
    cat /proc/cpuinfo|grep "cpu cores"|uniq
    #cpu cores : 2
```
###### /etc/nginx/nginx.conf
```nginx
    ...
    
    # 启动多少个nginx进程 一般和你的物理cpu数量 1*2
    worker_processes 2;
    # auto version > 1.9
    worker_cpu_affinity auto;
    ...
```
#### nginx通用配置优化
###### /etc/nginx/nginx.conf
```nginx
    # 设置nginx执行用户
    user nginx;
    
    # 启动多少个nginx进程 一般和你的物理cpu数量 1*2
    worker_processes 2;
    
    # auto version > 1.9
    worker_cpu_affinity auto;
    
    # 错误日志路径
    error_log /var/log/nginx/error.log warn;
    
    # 进程启动后pid 存放位置
    pid /var/run/nginx.pid
    
    # 文件句柄进程级别限制 ,小站点 1W左右，大一点的2W以上
    worker_rlimit_nofile 10240；
    
    # 事件驱动器模块
    events {
        # epoll模型
        use epoll; 
        
        # 限制每个worker 进程能够处理多少个连接 默认是1024,有点少
        worker_connections 10240;
    }
    
    http {
        # 包含所有的mime type
        include /etc/nginx/mime.types;
        # 设置默认的类型
        default_type application/octet-stream;
        
        # 字符集设置
        charset utf-8;
        
        log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
                      
        access_log /var/log/nginx/access.log main;
        
        # 对静态资源的处理是有效的 打开
        sendfile on;
        
        #开启gzip
        gzip on;

        # ie6 不支持gzip压缩
        gzip_disable "MSIE [1-6]\.";
        
        #gzip 版本
        gzip_http_version 1.1;
        
        
        include /etc/nginx/conf.d/*.conf
    }
```