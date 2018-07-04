# HTTP升级成HTTPS

自签名的实现步骤在这里具体步骤就不进行说明了,一般按照服务提供商的要求签名格式进行操作就可以了。我们介绍一种简单的https签名方式

## 用 Let's Encrypt 和 certbot 搭建 https

[打开 certbot 官网](https://certbot.eff.org/),选择服务器软件和系统 按照官方的实例进行按照,下面我提供下我服务器的按照步骤（我的是 NGINX+ CentOS6）

### 安装

由于CentOS6没有打包版本的Certbot，因此您应该使用certbot-auto脚本来获取副本：

```text
    wget https://dl.eff.org/certbot-auto
    chmod a+x certbot-auto
```

certbot-auto是和 certbot一样的; 它是一个包装器，可以安装所有自己的依赖项并自动更新客户端代码。

#### 注意：

certbot-auto将一直试图从其最新版本中获取最新版本的自身。如果您希望将其锁定到特定版本并且未收到自动更新，请使用--no-self-upgrade标志运行它 。另外，如果您对从网络上下载和运行脚本感到紧张，则可以使用一些[额外的验证步骤](https://certbot.eff.org/docs/install.html#certbot-auto)。

### 开始使用

Certbot有一个Nginx插件，它在许多平台上都受支持，并且安装了证书。

```text
    sudo ./path/to/certbot-auto --nginx
```

运行此命令将为您获得证书，并让Certbot自动编辑您的Nginx配置以便为其提供服务。如果您感觉更保守，并且想手动更改Nginx配置，则可以使用certonly 子命令：

```text
    sudo ./path/to/certbot-auto --nginx certonly
```

### 自动更新

Certbot可以配置为在证书过期之前自动续订您的证书。自从让我们将证书最后加密90天后，最好利用此功能。您可以通过运行以下命令来测试证书的自动续订：

```text
    sudo ./path/to/certbot-auto renew --dry-run
```

如果这似乎工作正常，您可以通过添加运行以下命令的[cron](http://www.unixgeeks.org/security/newbie/unix/cron-1.html)作业或[systemd](https://wiki.archlinux.org/index.php/Systemd/Timers)计时器来安排自动续订：

```text
    ./path/to/certbot-auto renew
```

#### 注意：

如果您正在设置cron或systemd作业，我们建议每天运行两次（在您的证书到期续约或撤消之前，它不会执行任何操作，但定期运行它可以让您的站点保持在线状态案例a让我们加密发起的撤销是由于某种原因发生的）。请在一小时内为您的续订任务选择一个随机分钟。

```text
    # 需要安装python
    0 0,12 * * * python -c 'import random; import time; time.sleep(random.random() * 3600)' && ./path/to/certbot-auto renew
```

