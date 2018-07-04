# HTTP字符串替换\( http\_sub\_module \)

## 配置语法

| http\_sub\_module | 字符串替换 |  | 替换一次 |
| :--- | :--- | :--- | :--- | :--- |
| 语法 | sub\_filter string replacement | sub\_filter\_last\_modified on \| of | sub\_filter\_once on \| off |
| 默认 | --- | sub\_filter\_last\_modified off | sub\_filter\_once on |
| 作用域 | http,server,location | http,server,location | http,server,location |

### 例子:

```text
    location / {
        root   /www/nginx/code; 
        # 将字符串 king 替换为 kingofzihua
        sub_filter 'king' 'kingofzihua';
        #全局替换，默认只会替换一次
        sub_filter_once off; 
    }

    # 注意，只能替换html文件,txt 文件不可以！ 而且只替换一次，如果要是全局替换的话要用sub_filter_once
```

