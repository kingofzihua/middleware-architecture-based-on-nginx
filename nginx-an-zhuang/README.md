# Nginx安装

nginx可以使用各平台的默认包来安装。

## 安装

### centOS安装

#### 安装 nginx

```text
    #centos 安装创建nginx yum 源
    vim /etc/yum.repos.d/nginx.repo

    #添加到文件 将OS替换为你的centos OSRELEASE替换为你的版本比如7 
    [nginx]
    name=nginx repo
    baseurl=http://nginx.org/packages/OS/OSRELEASE/$basearch/
    gpgcheck=0
    enabled=1

    #安装nginx
    yum install
```

### ubuntu安装

#### 安装 nginx

```text
    apt-get install nginx
```

