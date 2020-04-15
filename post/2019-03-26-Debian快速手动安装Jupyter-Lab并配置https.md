# Debian快速手动安装Jupyter Lab并配置https

很久之前我写过一篇关于`Jupyer lab`得超详细安装教程，[`传送门`](https://www.creat.kim/archives/25/)，感觉复杂了点，特别是`nginx`，我这块也没写清楚，所以不少人出现了无法运行`python`的情况，按照教程一步步来是绝对不会出问题的，虽然你能够用`https`访问，但是不代表就能运行，因为这里`jupyter lab`是基于`websocket`通信的，不是`http`。这里就再简化一下，用`Debian`系统安装一下`Jupyter Lab`，并使用`caddy`配置`https`访问，亲测可以运行程序。本教程只包括`Pytho2`内核，要同时安装`Python3`见[`传送门`](https://www.creat.kim/archives/25/)，这里简单写下步骤，快速上手，避免花费过多时间，一次成功，速度还蛮快的. demo: https://jupyter.creat.kim
![](http://image.creat.kim/picgo/20190326142651.png)
![](http://image.creat.kim/picgo/20190326151655.png)
```
sudo apt-get install software-properties-common
```
## 安装`Python`环境
```
sudo apt-get install python-pip python-dev build-essential 
sudo pip install --upgrade pip 
sudo pip install --upgrade virtualenv 
sudo apt-get install python-setuptools python-dev build-essential 
sudo easy_install pip 
sudo pip install --upgrade virtualenv 
sudo apt-get install python3-pip
sudo apt-get install python-pip
sudo pip3 install --upgrade pip
sudo pip2 install --upgrade pip
sudo pip install --upgrade pip
```
## 查看`pip`指向
```
~ $which pip
/usr/local/bin/pip
21:36 alien@alien-Inspiron-3443:
~ $which pip2
/usr/local/bin/pip2
21:36 alien@alien-Inspiron-3443:
~ $which pip3
/usr/local/bin/pip3
```
## 安装`yarn`
```
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update
sudo apt-get install yarn
```

## 安装`nodejs`
```
curl -sL https://deb.nodesource.com/setup_10.x | bash -
apt-get install -y nodejs
```

## 安装`jupyterlab`
```
sudo pip2 install jupyterlab
```

## 配置`jupyerlab`
```
jupyter-notebook password
```
进入`ipython`设置哈希密码，这里输入的是你登陆`jupyter lab`的密码，记下生成的哈希密码.
```
ipython
from notebook.auth import passwd
passwd()
# 输入你自己设置登录JupyterLab界面的密码，
# 然后就会生产下面这样的密码，将它记下来，待会儿用
'sha1:b92f3fb7d848:a5d40ab2e26aa3b296ae1faa17aa34d3df351704'
```

## 编辑配置文件
一般在`/root/.jupyter/jupyter_notebook_config.py`中，找到并修改以下配置项。
```
c.NotebookApp.allow_root = True
c.NotebookApp.ip = '0.0.0.0'
c.NotebookApp.notebook_dir = u'/root/JupyterLab'
c.NotebookApp.open_browser = False
c.NotebookApp.password = u'sha1:b92f3fb7d848:a5d40ab2e26aa3b296ae1faa17aa34d3df351704'
c.NotebookApp.port = 8888

# 解释以上各项
允许以root方式运行jupyterlab
允许任意ip段访问
设置jupyterlab页面的根目录
默认运行时不启动浏览器，因为服务器默认只有终端嘛
设置之前生产的哈希密码
设置访问端口，与下面的caddy需一致
```

## 运行`Jupyter Lab`
```
jupyter-lab --version
jupyter lab build

mkdir ~/JupyterLab
cd ~/JupyterLab

# 方便后台运行
apt install screen
screen -S jupterlab
jupyter lab 
```
`ctrl+A+D`退出这个窗口。

## `caddy`开启`https`反代

域名改成你自己的，`caddy`详细使用见：[`【传送门】`](https://www.creat.kim/archives/18/)
```
wget -N --no-check-certificate https://raw.githubusercontent.com/ds19991999/shell.sh/shell/caddy_install.sh && chmod +x caddy_install.sh && bash caddy_install.sh

echo "jupyter.creat.kim
 gzip
 tls cva.engineer.ding@gmail.com
 proxy / 127.0.0.1:8888 {
  transparent
  websocket
 }" > /usr/local/caddy/Caddyfile
```
## 定时备份到`GitHub`
见大佬写的比较详细的文章：[`【传送门】`](https://www.moerats.com/archives/858/)

## 配置`python2`和`python3`内核
好人做到底吧，这里肯定很多人踩坑。。。用`pip`安装包的时候千万不要用`pip3 install ***`或者`pip2 install ***`呀.
```
python2 -m pip install ipykernel ipython matplotlib scipy pandas numpy
python3 -m pip install ipykernel ipython matplotlib scipy pandas numpy
```
检查一下内核，看文件夹里的`Python`有没有指向错误，避免最后出现`Python2`和`Python3`内核全是`Python2`，主要是把文件夹内的`json`改成相应的`Python`版本即可.
```
root@google:~/JupyterLab# jupyter kernelspec list
Available kernels:
  python2    /usr/local/share/jupyter/kernels/python2
  python3    /usr/local/share/jupyter/kernels/python3
```
好了，访问域名，开始使用吧。

