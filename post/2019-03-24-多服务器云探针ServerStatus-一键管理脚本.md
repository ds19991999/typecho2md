# 多服务器云探针ServerStatus 一键管理脚本

某大佬的脚本...

## 系统要求
`CentOS 7 / Debian 7+ / Ubuntu 14.04 +` 推荐 `Debian 8 x64`
## 安装步骤
```
wget -N --no-check-certificate https://raw.githubusercontent.com/ds19991999/shell.sh/shell/status.sh && chmod +x status.sh
```
根据需要安装客户端或者服务端：
```
# 显示客户端管理菜单
bash status.sh c
 
# 显示服务端管理菜单
bash status.sh s
```
## 文件说明

```
安装目录：/usr/local/ServerStatus

网页文件：/usr/local/ServerStatus/web

配置文件：/usr/local/ServerStatus/server/config.json

客户端查看日志：tail -f tmp/serverstatus_client.log

服务端查看日志：tail -f /tmp/serverstatus_server.log
```
