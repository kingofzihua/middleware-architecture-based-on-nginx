# rewrite规则

## 实现url重写以及重定向

## 场景

* Url访问跳转,支持开发设计
  * 页面添砖、兼容性支持、展示效果等
* SEO优化
* 维护
  * 后台维护、流量转发等
* 安全

## 配置语法

| rewrite |  |
| :--- | :--- | :--- |
| 语法 | rewrite regex replacement \[flag\] |
| 默认 | --- |
| 作用域 | server,location,if |
| 例如 | 将网站所有请求全部重定向一个页面    rewrite ^\(.\*\)$ /page/maintain.html break |

## 正则表达式

| 正则表达式 |  |
| --- | --- |
| . | 匹配除换行符以外等任意字符 |
| ? | 重复0次或1次 |
| + | 重复1次或更多次 |
| \* | 匹配前面的子表达式零次或多次 |
| \d | 匹配数字 |
| ^ | 匹配字符串的开始 |
| $ | 匹配字符串的结尾 |
| {n} | 重复n次 |
| {n,} | 重复n次或更多次 |
| \[c\] | 匹配单个字符串c |
| \[a-z\] | 匹配a-z小写字母的任意一个 |
| \ | 转移字符 |
| \( \) | 用于匹配括号之间的内容,通过$1、$2调用 |

### 例子:

```text
   ...

   if($http_user_agebt ~ MSIE) {
       rewrite ^(.*)$ /msie/$1 break;
   }

   ...
```

## pcretest

pcretest是一个正则表达式测试工具

### 例子:

```text
    $ pcretest #回车
    PCRE version 8.36 2014-09-29 #这个是命令行显示的pcre版本

       re> /(\d+)\.(\d+)\.(\d+)\.(\d+)/ #输入所要匹配的正则 然后回车
    data> 192.168.10.10
    0: 192.168.10.10
    1: 192
    2: 168
    3: 10
    4: 10
```

## flag

| flag |  | 备注 |
| --- | --- | --- |
| last | 停止rewrite检测 | last停止后重新创建一个请求，然后跳转 |
| break | 停止rewrite检测 | break直接寻找重写后的文件 |
| redirect | 返回302临时重定向,地址栏会显示跳转后的地址 |  |
| permanent | 返回301永久重定向,地址栏会显示跳转后的地址 |  |

### 例子:

```text
    ...

    root /www/nginx/code/

    location ~ ^/break {
        # 这个匹配到了以后 会往 /www/nginx/code/test/ 下寻找有没有 并停止
        rewrite ^/break /test/ break;
    }

    location ~ ^/last {
     # 这个匹配到了以后会重新发起一次请求 访问 uri/test/
        rewrite ^/last /test/ last;
    }

    location /test/ {
        default_type application/json;
        return 200 '{"status":"success"}'
    }

    ...

    # 访问 kingofzihua.top/break 会返回403 
    # kingofzihua.top 是我配置的虚拟域名
    # 返回403是因为我 并没有/www/nginx/code/test/ 这个目录

    # 访问 kingofzihua.top/last 会返回{"status":"success"};
    # 因为它重新发起了一次请求 kingofzihua.top/test/ 

    location /course {
        root   /www/nginx;
        # 访问 /coutse-01-02-03.html 转化为 /coutse/01/02/coutse_03.html
        rewrite ^/coutse-(\d+)-(\d+)-(\d+)\.html$ /course/$1/$2/course_$3.html break;

        # 判断如果是Chrome浏览器就跳转到百度
        if ($http_user_agent ~* Chrome) {
            # 如果访问的匹配到nginx 就跳转到百度搜索nginx
            rewrite ^/nginx https://www.baidu.com/s?wd=nginx;
        }

        # 判断如果不是一个目录
        if (!-f $request_filename ) {
            # /index 重写为index.php?s=/index
            rewrite ^(.*)$ /index.php?s=$1 last;
        }
    }

    ...
```

## Rewrite规则优先级

* 执行server块的rewrite指令
* 执行location匹配
* 执行选定的location中的rewrite

