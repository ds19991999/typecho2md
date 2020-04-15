# KindleEar+RSSHub+Kindle——个人阅读解决方案

## 说明
`KindleEar`是一个运行在`Google App Engine（GAE）`上的`Kindle`个人推送服务应用，生成排版精美的杂志模式`mobi / epub`格式自动每天推送到您的`Kindle`或其他邮箱。demo: https://kindle-236923.appspot.com

`RSSHub`则是一个轻量，易于扩展的RSS生成器，可以给任何奇奇怪怪的内容生成RSS订阅源。可以利用[`Heroku`](https://www.heroku.com/)部署. `Heroku`则是一个提供免费`web`应用部署的平台。注意，`Heroku`免费账户部署的`web`应用超过`30`分钟没有使用就会休眠，而这里[`GitHub`学生包](https://education.github.com/pack)则给我们免费提供两年`Heroku`的付费账户，额度有`160$`. demo: https://moerss.herokuapp.com/

![](https://i.loli.net/2019/04/08/5cab03ffed6c3.png)

![](https://i.loli.net/2019/04/08/5cab05b318e41.png)

## `KindleEar` 
> github: https://github.com/cdhigh/KindleEar

创建一个`gce app`： https://console.developers.google.com/project
转到`gcp`，激活`shell`, 全选复制以下命令，按照提示输入 Gmail 和 APPID 即可轻松上传。
```
rm -f uploader.sh* && \
wget https://raw.githubusercontent.com/kindlefere/KindleEar-Uploader/master/uploader.sh && \
chmod +x uploader.sh && \
./uploader.sh
```

## `RSSHub`
> github: https://github.com/DIYgod/RSSHub

`Heroku`部署：https://elements.heroku.com/buttons/diygod/rsshub
使用方法：RSSHub服务器+RSSHub路由，eg: https://rss.creat.kim/rsshub/rss

## 订阅`RSS`源/路由

`RSSHub`：`/rsshub/rss`
`Typora`：`/typora/changelog`

### 高分电影

豆瓣高分电影：`/douban/movie/playing/7.5/广州`
草榴社区动漫原创区：`/t66y/5`
电影首发站：`/dysfz`
电影天堂：`/dytt`
人生 05 电影：`/rs05/rs05`
高清电台最新电影：`/gaoqing/latest`
JavBus：`/javbus/home`
Mp4Ba电影：`/mp4ba/1`

### 漫画动漫
pixiv 月排行：`/pixiv/ranking/month/`
Bangumi：`/bangumi/calendar/today`
忧郁的 `loli`：`/mmgal`
终点分享：`/zdfx`
動畫瘋：`/anigamer/new_anime`
Animen 动漫平台：`/animen/news/dh`
`ebb.io`：`ebb.io`


### 编程资讯
掘金分类后端热门：`/juejin/trending/backend/monthly`
Dockone：`/dockone/weekly`
V2EX最热主题：`/v2ex/topics/hot`
GitLab Explore: `/gitlab/explore/trending`
安全客最新漏洞列表: `/aqk/vul`
看雪最新密码算法:`/pediy/topic/crypto/latest`
Gitea：`/gitea/blog`
LeetCode：`/leetcode/articles`
V2EX - LeetCode：`https://www.v2ex.com/feed/leetcode.xml`
V2EX - Python：`https://www.v2ex.com/feed/python.xml`
思否后端频道：`/segmentfault/channel/backend`
V2ex Linux: `https://www.v2ex.com/feed/linux.xml`
V2EX - shadowsocks: `https://www.v2ex.com/feed/shadowsocks.xml`

### 博客订阅
Rat's Blog：`https://www.moerats.com/feed`
如有乐享：`https://51.ruyo.net/feed/`
神代綺凜の萌化小基地：`https://moe.best/feed`
编程随想的博客：`http://feeds.feedburner.com/programthink`

### 新闻杂志
纽约时报：`/nytimes/index/dual`
Solidot:`/solidot/linux`
极客公园:`/geekpark/breakingnews`
联合国政务消息:`/un/scveto`
中国政府政务消息：`/gov/zhengce/zuixin`
Readhub：`readhub/category/technews`
果壳网：`/guokr/scientific`
经济学人：`https://github.com/nailperry-zd/The-Economist/commits.atom`

### 个人博客
C.K:`https://www.creat.kim/feed/`
C.K 的评论:`https://www.creat.kim/feed/comments/`
ds19991999的博客:`https://blog.csdn.net/ds19991999/rss/list`

## OPML 文件
![](https://i.loli.net/2019/04/08/5cab1250d155b.png)
支持直接导入RSS源的OPML文件：https://git.io/rss.xml