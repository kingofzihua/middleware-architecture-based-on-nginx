# 日志模块 \(log\_module\)

包括 error access.

## 配置语法

| log\_format |  |
| :--- | :--- | :--- |
| 语法 | log\_format name \[escape=default \| json\] string ... |
| 默认 | log\_format combined "..." |
| 作用域 | http |

### 例子:

```text
    # 错误日志
    error_log  /var/log/nginx/error.log warn;
    # /var/log/nginx/error.log : log文件位置 | warn : 记录warn及其以上等级的日志
    # 错误等级 : debug info notice warn error crit 

    #定义一个 log_format | 名字为main | 记录的字符串模版
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    # 成功日志
    access_log  /var/log/nginx/access.log  main;
    # /var/log/nginx/access.log : log文件位置 | main ： log_format的名字 表示记录格式
```

