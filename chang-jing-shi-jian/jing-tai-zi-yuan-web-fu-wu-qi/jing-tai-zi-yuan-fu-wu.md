### 静态资源服务
#### 静态资源服务
![image](https://kingofzihua.oss-cn-shanghai.aliyuncs.com/blog/nginx/static_resources_web_server.png)
#### 静态资源类型
| 类型 | 种类 |
| ---  | --- |
| 浏览器端渲染 | HTML、CSS、JS |
| 图片 | JPEG、GIF、PNG |
| 视频 | FLV、MPEG |
| 文件 | TXT、等任意下载文件 |
#### 静态资源服务场景-CDN
![image](https://kingofzihua.oss-cn-shanghai.aliyuncs.com/blog/nginx/static_resources_web_server_cdn.png)

#### 配置语法
| 静态资源服务 |   |   |  |
| :-------- | :---- | :---- | :---- | 
| 语法   | sendfile on \| off | tcp_nopush  on \| off | tcp_nodelay on \| off | 
| 默认   | sendfile off | tcp_nopush off | tcp_nopush on | 
| 作用域 | http,server,location, if in location | http,server,location |  http,server,location |
| 备注 |  | sendfile开启的情况下,提高网络包的传输效率 | keepalive连接下,提高网络包的传输实时行 | |