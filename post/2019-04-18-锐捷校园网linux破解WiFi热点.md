# 锐捷校园网linux破解WiFi热点

首先锐捷校园网本身是不支持开热点的，所以就有了linux下的折腾.
## mentohust认证
下载地址：[mentoshut](https://linux.linuxidc.com/index.php?folder=MjAxM8Tq18rBzy8x1MIvMjDI1S9VYnVudHXPwsq508NNZW50b0hVU1S0+szmyPG93cjP1qTJz834)

```
# 安装就不说了
sudo apt-get install mentohust
# 启用后台认证
sudo mentohust -uusername -p123456 -a1 -d2 -b2 -v4.10 -w
# 关闭认证
sudo mentohust -k 
```
## 编辑脚本
假设把脚本放在`/home/$USER/app/`目录下面：
```
cat > /home/$USER/app/net
#!/bin/bash
sudo mentohust -uusername -p123456 -a1 -d2 -b2 -v4.10 -w

ctrl+c退出
sudo chmod -R 777 /home/$USER/app
```
## 添加可执行文件路径
```
sudo echo "export PATH="$PATH:/home/$USER/app" >> /etc/profile
sudo echo "export PATH="$PATH:/home/$USER/app" >> ~/.profile
sudo echo "export PATH="$PATH:/home/$USER/app" >> ~/.bashrc
```
现在可以直接输入`net`来认证校园网了。

## 开启热点
> github: https://github.com/oblique/create_ap

### 安装create_ap
```
#安装hostapd
apt-get install hostapd

#安装create_ap
git clone https://github.com/oblique/create_ap
cd create_ap
make install

sudo systemctl start NetworkManager
```
### 尝试开启热点
查看本机网卡名称：
```
sudo iwconfig

```
![](https://raw.githubusercontent.com/ds19991999/image/master/picgo/20190418145659.png)
修改该文件夹下的配置文件：
```
sudo vi create_ap.conf
WIFI_IFACE=wlp6s0 # 无线网卡名称
INTERNET_IFACE=enp7s0 # 有线网卡名称
SSID=debian   # 显示的热点名称
PASSPHRASE=12345678 # 热点密码，必须是8位数以上
```
![](https://raw.githubusercontent.com/ds19991999/image/master/picgo/20190418145411.png)

尝试开启wifi:
```
# 后面四个参数尽量与上面一致
sudo create_ap wlp6s0 enp7s0 debian 12345678
# 如果手机能连上debian这个热点说明开启成功
```
修改配置文件
```
sudo vi /etc/create_ap.conf
# 与上面四个参数保持一致
```
### 配置开机自启
```
sudo systemctl enable create_ap
sudo service create_ap start 
```
## 相关文章
* [debian自用装机配置](https://www.creat.kim/archives/65/)
* [常用命令行下载器](https://www.creat.kim/archives/81/)
* [U盘上的kali装机配置](https://www.creat.kim/archives/80/)