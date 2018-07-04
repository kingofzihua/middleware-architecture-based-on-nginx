# Lua

是一个简介、轻量、可扩展的脚本语言

## lua的基础语法

### 安装

```text
    yum install lua
```

### 运行

```text
    # lua
    Lua 5.1.1 Copyright(C) 1994-2008 Lua.org,PUC-Rio
    >print('Hello world')
    Hello world


    #lua ./test.lua
    Hello world
```

### 注释

```lua
    -- 行注释

    --[[
        块注释
    --]]
```

### 变量

```lua
    a='alo\n123'
    a="alo\n123\""
    a='alo\n123\"'
    a=[[alo
    123"]]
    #布尔类型只有nil和false是false,数字0，空字符串 都是true
    #lua中的变量如果没有特殊说明,全是全局变量
```

### 基础语法

while循环语句

```lua
    sum=0
    num=1
    while num <=100 do
        sum = sum + num
        num = num + 1
    end

    print("sum = ",sum)
```

for循环语句

```lua
    sum=0
    for i=1,100 do
        sum = sum + i
    end
```

if-else 判断语句

```lua
    if age == 40 and sex == "Male" then
        print("等于40的男人")
    elseif age >60 and sex ~= "Female" then
        print("大于60 并且不是女人")
    else
        local age =io.read()
        print("Your age is"..age)
    end

    # "~=" 是不等于
    # 字符串的拼接操作 ".."
    # io库 分别从stdin和stdout读写的read和write函数
```

