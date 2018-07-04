# HTTP状态管理\(http\_stub\_status\_module\)

## 配置语法

| http\_stub\_status\_module |  |
| :--- | :--- | :--- |
| 语法 | stub\_status |
| 默认 | --- |
| 作用域 | server,location |

### 例子:

```text
   # 配置一个匹配规则，当访问当url是 /mystatus 就返回 stub_status
   location /mystatus {
       stub_status;
   }
   # 前台显示:
   # Active connections: 2 
   # server accepts handled requests
   # 9 9 40 
   # Reading: 0 Writing: 1 Waiting: 1
```

