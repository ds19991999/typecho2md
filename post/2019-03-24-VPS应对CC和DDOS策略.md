# VPS应对CC和DDOS策略

```
## 查看单个IP的连接数
netstat -nat|grep -i '80'|wc -l
# 连接的IP按连接数量进行排序，查看TCP连接状态
netstat -ntu | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -n
```
## 启用`Cloudflare`防攻击模式
[链接](https://www.daniao.org/3773.html)
效果`Cloudflare`经典5秒：
![](http://image.creat.kim/picgo/20190325141928.png)