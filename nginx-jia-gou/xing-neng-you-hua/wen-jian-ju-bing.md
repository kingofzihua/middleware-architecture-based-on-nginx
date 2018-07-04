# 文件句柄

Linux\Unix一切皆文件,文件句柄就是一个索引

## 设置方式

系统全局性修改、用户局部性修改、进程局部性修改

### 例子:

#### /etc/security/limits.conf

```text
    # 文件具柄
    # 针对root用户 用户局部性修改
    root sofa nofile 65535
    root hard nofile 65535

    # 针对所有用户 系统全局性修改
    *    soft nofile 25535
    *    hard nofile 35535
```

#### /etc/nginx/nginx.conf

```text
    ...

    # nginx进程局部性修改
    worker_rlimit_nofile 35535;

    ...
```

