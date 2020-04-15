# iptables string模块屏蔽泛域名(匹配字符串)

一些人不想让别人用`Shadowsocks`账号访问指定域名，但是通过`Hosts`屏蔽域名的话比较麻烦，`Shadowsocks`服务端是启动的时候才会读取`Hosts`，所以每次修改都需要重启`Shadowsocks`服务端，并且`Hosts`的方法屏蔽域名，只支持单域名，并不支持泛域名，很不方便。

## 示例
屏蔽以 `youtube.com` 为主的所有一级 二级 三级等域名。
```
iptables -A OUTPUT -m string --string "youtube.com" --algo bm -j DROP
# 添加屏蔽规则
 
iptables -D OUTPUT -m string --string "youtube.com" --algo bm -j DROP
# 删除屏蔽规则，上面添加的代码是什么样，那么删除的代码就是把 -A 改成 -D 
```
## 解释
```
-A
# 添加iptables规则；
-D
# 删除iptables规则（把添加防火墙规则时代码中的 -A 改成 -D 即可删除添加的规则）；
-m string
# 指定模块；
--string "youtube.com"
# 指定要匹配的字符串(域名、关键词等)；
--algo bm
# 指定匹配字符串模式/算法（还有一种更复杂的算法：kmp）；
-j DROP
# 指匹配到数据包后处理方式，这里是丢弃数据包。
```
