# JSProxy+CloudFlare 实现免费爬墙

 GitHub: https://github.com/EtherDream/jsproxy

说明：昨天看到如有乐享的博主分享了一个利用 `CloudFlare` 和 `JSProxy` 实现的免费翻墙服务。目前国内并没有对`CloudFlare`  的`ip` 进行封锁，而`cf` 又给我们提供了免费`cdn` 服务，现在又出现了`JSProxy`这种新的爬墙方式，羊毛还是比较多的。`JSProxy` 这个项目之前在 [TG](https://t.me/baba2333) 频道分享过，当时觉得用服务器搭建有点浪费，所以就没弄，现在出现这种直接对`cloudflare` 的 `cdn` 编程的方式实现爬墙确实让人心动，于是就搭了一个玩玩。

> demo: https://jsproxy.creat.workers.dev

![](https://image.creat.kim/picgo/20190721104737.png)

![](https://image.creat.kim/picgo/20190721104835.png)

## 准备工作
[cloudflare](https://dash.cloudflare.com) 账号一枚，申请就不用说了。

## 创建Workers

进入 https://workers.cloudflare.com 自定义前缀激活 workers 服务，比如我的就是 `creat.workers.dev` 。然后就创建一个 `worker` , 自定义前缀，比如我的就是 `jsproxy.creat.workers.dev` ，然后在左侧栏粘贴js代码：https://raw.githubusercontent.com/EtherDream/jsproxy/master/cf-worker/index.js

![](https://image.creat.kim/picgo/20190721105659.png)

点击部署九可以用了。

## 限制
每天限制`100000` 次请求，够用了。
![](https://image.creat.kim/picgo/20190721105932.png)