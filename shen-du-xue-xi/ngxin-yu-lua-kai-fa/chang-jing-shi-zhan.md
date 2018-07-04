# 场景实战

按照一定的关系区别,分部分的代码进行上线,使代码的发布能平滑过渡上线。

* 用户的信息cookie等信息区别
* 根据用户的ip地址

## 流程

![](https://kingofzihua.oss-cn-shanghai.aliyuncs.com/blog/nginx/grayscale-release.png)

### 例子:

#### 安装lua memcache 模块

```text
    wget https://github.com/agentzh/lua-resty-memcached/archive/v0.11.tar.gz
    tar -zxvf v0.11.tar.gz
    pc -r lua-resty-memcached-0.11/lib/resty /usr/local/share/lua/5.1/
```

#### /opt/app/lua/dep.lua

```lua
    --获取客户端的IP
    clientIP = ngx.req.get_headers()["X-Real-IP"]
    --如果clientIP为空 则从x_forwarded_for获取
    if clientIP ==nil then
        clientIP = ngx.req.get_headers()["x_forwarded_for"]
    end

    --如果clientIP还为空 则从remote_addr获取
    if clientIP ==nil then
        clientIP = ngx.var.remote_addr
    end
        --lua 调用 memcached
        local memcached = require "resty.memcached"
        local memc ,err = memcached:new()
        if not memc then
            ngx.say("failed to instantiate memc: ",err)
            return
        end
        -- 连接memcached
        local ok,err = memc:connect("127.0.0.1",11211)
        if not ok then
            ngx.say("failed to connect: ",err)
            return
        end
        -- 从 memcached 获取 clientIP
        local res,flags,err =memc:get(clientIP)
        ngx.say("value key: ",res,clientIP)
        if err then
            ngx.say("failed to get clientIP ",err)
            return
        end
        -- 如果从memcached取出来的是 1 
        if res == "1" then
            --@server_test 看nginx定义的！
            ngx.exec("@server_test")
            return
        end 
        --@server 看nginx定义的！
        ngx.exec("@server")
```

#### /etc/nginx/conf.d/default.conf

```text
    ...

    location / {
        default_type 'test/html';
        # 读取lua文件处理
        content_by_lua_file '/opt/app/lua/dep.lua';
    }

    # 端口转发给9090
    location @server {
        proxy_pass http://127.0.0.1:9090;
    }

    # 端口转发给8080
    location @server_test {
        proxy_pass http://127.0.0.1:8080;
    }

    ...
```

