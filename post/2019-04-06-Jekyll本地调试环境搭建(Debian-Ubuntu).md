# Jekyll本地调试环境搭建(Debian/Ubuntu)

## 安装Ruby
Ruby 官网中文文档：[传送门]( http://www.ruby-lang.org/zh_cn/documentation/installation/)
切换淘宝ruby源
```
gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
gem sources -l
```
安装
```
sudo apt-get install ruby-full
```

## Jekyll安装
Jekyll 官网（中文）： http://jekyll.com.cn/ 
Jekyll 官网： https://jekyllrb.com/
```
# 安装jekyll和编译环境
gem install jekyll bundler
# 新建一个站点
jekyll new myblog && cd myblog
# 编译站点开启web服务
bundle exec jekyll serve
```
查看端口占用
```
netstat -lntp | grep 4000
kill -9 [PID]
```
## Jekyll-Admin
在`_config.yml`的`gem`一行添加一个`jekyll-admin`
```
gems: [jekyll-paginate, jekyll-sitemap,jekyll-admin]
```
运行
```
gem install jekyll-admin
```
访问
```
http://localhost:4000/admin
```


