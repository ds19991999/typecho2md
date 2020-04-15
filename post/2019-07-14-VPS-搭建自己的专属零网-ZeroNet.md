# VPS 搭建自己的专属零网 ZeroNet

说明：最近都没什么新东西写了，随便翻了一下以前整理的资源，发现零网上面的东西相对来说还是蛮多的，目前网上搭建零网的教程很少，大部分都是在本地运行，少有几篇采用`VPS`搭建，不过，也是用了`nginx`反代，没有 `Caddy` 方面的教程。于是就尝试了一下采用比较轻量的 `Caddy` 反代端口配置域名和`https`。本以为蛮简单的，结果还是遇到了不少坑，记录一下。

> - ZeroNet：https://github.com/HelloZeroNet/ZeroNet
>
> - zeronet-tracker：https://github.com/ZeroNetJS/zeronet-tracker


![](https://image.creat.kim/picgo/20190714211214.png)
## 下载源码

```shell
apt update
apt install msgpack-python python-gevent screen
wget https://github.com/HelloZeroNet/ZeroNet/archive/master.tar.gz
tar -zxvf master.tar.gz
rm master.tar.gz
cd ZeroNet-master
```

## 配置零网

将`plugins/disabled-UiPassword`目录重命名为`plugins/UiPassword` ，启用密码登录零网。

![](https://image.creat.kim/picgo/20190714190836.png)

首次直接运行`python zeronet.py --ui_ip "*"`，然后访问`http://yourip:43110`就可以了，不过这样任何人都能访问，不太安全。`kill` 掉之后，编辑`zeronet.conf`

```shell
vim zeronet.conf
# 添加如下几行
ui_password = 设置网站登录密码
ui_ip = 0.0.0.0
ui_host = 设置你绑定的域名，需要提前设置好DNS解析
ui_restrict = 127.0.0.1
```

## 后台运行 `ZeroNet`

```shell
# 服务器后台运行零网
nohup python zeronet.py & > /tmp/zeronet.log
```

访问`http://yourip:43110`，输入密码就可以登录网站。

![](https://image.creat.kim/picgo/20190714163627.png)

## `Caddy` 反代 `ZeroNet`

```shell
wget -N --no-check-certificate https://raw.githubusercontent.com/ds19991999/shell.sh/shell/caddy_install.sh && chmod +x caddy_install.sh && bash caddy_install.sh

echo '你的域名 {
 gzip
 header / Strict-Transport-Security "max-age=31556926"
 header / X-Frame-Options "SAMEORIGIN"
 header / X-XSS-Protection "1; mode=block"
 tls 你的真实邮箱 {
  alpn http/1.1
 }
 proxy / 127.0.0.1:43110 {
  transparent
  websocket
 }
}' > /usr/local/caddy/Caddyfile

# 如果上条命令运行不成功，请手动将内容复制到/usr/local/caddy/Caddyfile , 然后重启caddy
# 启动：/etc/init.d/caddy start
# 停止：/etc/init.d/caddy stop
# 重启：/etc/init.d/caddy restart
# 查看状态：/etc/init.d/caddy status
```

好了，访问你的域名，输入密码，就可以使用 `ZeroNet` 了。

![](https://image.creat.kim/picgo/20190714192356.png)

## 推荐两个网站

玩零网必看的两个神站

- 零网导航：http://127.0.0.1:43110/0cnguide.bit 
- 神`key`：http://127.0.0.1:43110/keys.bit

## 参考

- https://github.com/HelloZeroNet/ZeroNet/issues/1307
- [ZeroNet-Wiki](https://github.com/HelloZeroNet/ZeroNet/wiki/%E5%9C%A8VPS%E4%B8%8A%E5%AE%89%E8%A3%85ZeroNet)