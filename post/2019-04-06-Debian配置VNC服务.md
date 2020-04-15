# Debian配置VNC服务

## 服务端
### 添加sodo非root用户
```
sudo useradd alien -m
sudo passwd alien
sudo usermod -a -G adm alien
sudo usermod -a -G sudo alien
chmod 777 /etc/sudoers
# 添加
alien   ALL=(ALL)     ALL
```
### 安装VNC服务
```
sudo apt update
sudo apt install xfce4 xfce4-goodies
sudo apt install tightvncserver
```
### 配置vncserver
```
# 初始化
vncserver
# 关掉初始化的服务
vncserver -kill :1
```
配置脚本
```
mv ~/.vnc/xstartup ~/.vnc/xstartup.bak

vi ~/.vnc/xstartup
# 写入以下内容
#!/bin/bash
xrdb $HOME/.Xresources
startxfce4 &

sudo chmod +x ~/.vnc/xstartup
```
重新启动VNC服务器
```
vncserver
```
## 本地连接VNC server
```
# alien为vps sood非root用户
ssh -L 5901:127.0.0.1:5901 -C -N -l alien ip
```
然后本地用vnc客户端输入：
```
localhost:5901
```
连接后，您将看到默认的`Xfce`桌面。


