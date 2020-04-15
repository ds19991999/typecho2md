# Debian手动安装Typecho

今天搭了一个`Handsome`主题的博客，就简单写一下手动安装的流程。


<!--more-->

## 准备安装环境
安装必要软件

```
apt-get install -y wget screen curl git unzip
```

安装 `LNMP` 环境

```
screen -S lnmp
wget http://soft.vpser.net/lnmp/lnmp1.5.tar.gz -cO lnmp1.5.tar.gz && tar zxf lnmp1.5.tar.gz && cd lnmp1.5 && ./install.sh lnmp
```
版本都用默认的就好了，满足`Typecho`环境，记住自己输入的`MySQL`密码然后`Ctrl+A+D`退出这个窗口，让他后台安装，大概半个多小时.

等他大概出现这个样子就是安装完成了。看有没有提示安装失败.
```
+------------------------------------------------------------------------+
|          LNMP V1.5 for Debian Linux Server, Written by Licess          |
+------------------------------------------------------------------------+
|           For more information please visit https://lnmp.org           |
+------------------------------------------------------------------------+
|    lnmp status manage: lnmp {start|stop|reload|restart|kill|status}    |
+------------------------------------------------------------------------+
|  phpMyAdmin: http://IP/phpmyadmin/                                     |
|  phpinfo: http://IP/phpinfo.php                                        |
|  Prober:  http://IP/p.php                                              |
+------------------------------------------------------------------------+
|  Add VirtualHost: lnmp vhost add                                       |
+------------------------------------------------------------------------+
|  Default directory: /home/wwwroot/default                              |
+------------------------------------------------------------------------+
|  MySQL/MariaDB root password: 你之前输入的MySQL密码                          |
+------------------------------------------------------------------------+
+-------------------------------------------+
|    Manager for LNMP, Written by Licess    |
+-------------------------------------------+
|              https://lnmp.org             |
+-------------------------------------------+
```

## 配置`Typecho`网站
```
lnmp vhost add  
```
然后按照提示选`Typecho`，自定义数据库名，数据库用户名和密码.

## 上传`Typecho`文件
一般是将源码放在`/home/wwwroot/域名/`文件夹下. 官网是： http://typecho.org/download
## 安装`Typecho`
直接按照指南安装，填好之前自己的`MySQL`数据库信息，基本上就安装完了.

## 设置`http 301` 重定向强制`https`
修改：`/usr/local/nginx/conf/vhost/域名.conf `，将监听`80`端口的`server`代码段替换为下面这样。
```
server {
	listen 80;
	server_name www.creat.kim;
	return 301 https://www.creat.kim$request_uri;
}
```
修改完后运行`/etc/init.d/nginx restart` 重启`nginx`，使其生效，这样就能强制`https`访问网站了.

## 续期 `Let's Encrypt SSL`
```
root@aliyun:~# lnmp ssl add
+-------------------------------------------+
|    Manager for LNMP, Written by Licess    |
+-------------------------------------------+
|              https://lnmp.org             |
+-------------------------------------------+
Please enter domain(example: www.lnmp.org): www.creat.kim
 Your domain: www.creat.kim
Enter more domain name(example: lnmp.org *.lnmp.org): www.creat.kim
 domain list: www.creat.kim
Please enter the directory for domain www.creat.kim: /home/wwwroot/www.creat.kim
Allow Rewrite rule? (y/n) y
Please enter the rewrite of programme,
wordpress,discuzx,typecho,thinkphp,laravel,codeigniter,yii2 rewrite was exist.
(Default rewrite: other): typecho
You choose rewrite: typecho
Allow access log? (y/n) y
Enter access log filename(Default:www.creat.kim.log):
You access log filename: www.creat.kim.log
Enable PHP Pathinfo? (y/n) y
Enable pathinfo.
1: Use your own SSL Certificate and Key
2: Use Let's Encrypt to create SSL Certificate and Key
Enter 1 or 2: 2
It will be processed automatically.
/usr/local/acme.sh/acme.sh [found]
Removing exist domain certificate...
Starting create SSL Certificate use Let's Encrypt...
```
## Typecho整站定时备份到`GitHub`
见大佬写的比较详细的文章：[`【传送门】`](https://www.moerats.com/archives/858/)
