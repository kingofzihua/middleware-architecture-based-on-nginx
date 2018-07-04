# 随机主页 \(http\_random\_index\_module\)

## 配置语法

| http\_random\_index\_module |  |
| :--- | :--- | :--- |
| 语法 | random\_index on \| off |
| 默认 | random\_index off |
| 作用域 | location |

### 例子:

```text
    location / {
        root   /www/nginx/code; #随机读取/www/nginx/code下一个文件来显示
        random_index on;
    }

    # 特别注意！！！！
    # 如果我设置的 location 是 /random 则实际访问的是/www/nginx/code/random 这个路径下的文件是随机读取的！
```

