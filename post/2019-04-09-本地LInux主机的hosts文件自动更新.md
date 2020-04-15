# 本地LInux主机的hosts文件自动更新

 github:https://github.com/levinit/adhosts

## hosts 来源
```
https://raw.githubusercontent.com/googlehosts/hosts/master/hosts-files/hosts
https://adaway.org/hosts.txt
https://raw.githubusercontent.com/vokins/yhosts/master/hosts
https://raw.githubusercontent.com/ds19991999/shell.sh/shell/custom_host
```
## 安装脚本
需要`root`权限
```
chmod 777 /etc/hosts
wget https://git.io/newhosts
mv newhosts update-hosts
bash update-hosts
```
第一次运行成功之后，脚本会自动添加到`/usr/local/bin`目录，以后就可以在任意目录执行`update-hosts`命令进行`hosts`文件更新。