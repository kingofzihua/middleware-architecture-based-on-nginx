### geoip_module模块
 基于ip地址匹配MaxMind GeoIp 二进制文件,读取ip所在地域信息。
 
#### 安装

```shell
    # yum 安装nginx geoip模块
    yum install nginx-module-geoip
    
    # 下载geoIP 地域文件
    wget http://geolite.maxmind.com/download/geoip/database/GeoLiteCountry/GeoIP.dat.gz
    wget http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz
```
#### 使用场景
- 区别国内外作HTTP访问规则 
- 区别国内城市地域作HTTP访问规则


##### 例子:
```nginx
    # nginx.conf 加载第三方的模块
    load_module "modules/ngx_http_geoip_module.so";
    load_module "modules/ngx_stream_geoip_module.so";

    ...
    
    # 之前下载的GeoIP地域文件地址
    geoip_country /etc/nginx/geoip/GeoIP.dat;
    geoip_city /etc/nginx/geoip/GeoLiteCity.dat;
    
    server{
        ...
        
        location / {
            # 如果不是国内的服务器 就返回403
            if ($geoip_country_code != CN) {
                return 403;
            }
            
            root /usr/share/nginx/html;
            index index.php index.html index.htm
        }
        
        # 获取当前访问的IP
        location /myIp {
            default_type text/plain;
            return 200 "$remote_addr $geoip_country_name $geoip_country_code $geoip_city";
            # 输出 1.198.216.102 China CN ZhengZhou
        }
        ...
    }
    
    ...
```