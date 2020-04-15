# 命令行版Google Translate

介绍一个谷歌翻译的命令行工具.

> github: https://github.com/soimort/translate-shell

## 安装
```
# Archlinux
sudo pacman -S translate-shell

# Debian/Ubuntu/Linux Mint
sudo apt-get install translate-shell

# Fedora
sudo dnf install translate-shell

# 直接下载
wget git.io/trans
chmod + x trans
sudo mv trans /usr/local/bin/
```

## 简单使用
```
# 默认英译汉
trans English
# 汉译英
trans zh:en 中文
# 英译汉
trans en:zh English

# 查看支持的语言
trans -R

# 翻译成指定语言
trans :en "வணக்கம். எப்படி இருக்கீங்க?"
Hello.  How are you?

# 翻译指定语言到指定语言
trans zh:en "你怎么样,வணக்கம். எப்படி இருக்கீங்க?"
How are you, oh. எப்படி இருக்கீங்க?
# 翻译网页
trans en:zh http://www.w3.org/

冒号左右可以用+支持更多语言
左边即为要指定翻译的语言
右边即为要翻译成什么语言

参数
-j 视为翻译句子
-b 简短模式 @表示启用语音提示
trans -b :@ja "Saluton, Mondo"
-d 字典模式 -v 分页显示
-id 识别语言
-i 指定输入为文件

# 交互式翻译，这个比较好用
# 通常加上-b(简单模式)或者-d(字典模式使用)
trans -shell
```
相关文章：[无道词典](https://www.creat.kim/archives/81/#wudao-dict)