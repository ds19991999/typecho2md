# Linux的nano简单使用

## `nano`编辑器
### 安装
```
# CentOS 系统：
yum install nano -y
# Debian/Ubuntu 系统：
apt-get install nano -y
```
### 使用
**打开文件**
```
nano 文件名或文件绝对路径
 
例如：
nano /root/doubi.txt
nano doubi.txt
```
> 注意：当你打开一个不存在的文件，那么即为新建文件。

**光标控制**
移动光标：使用用方向键移动。
选择文字：按住鼠标左键拖动（然后就可以复制了）。

**复制文本**
这取决于你用的是什么SSH软件。
`Putty` 要复制文本则是点击鼠标左键选择要复制的文本即可。
`Xshell` 要复制文本则是点击鼠标左键选择要复制的文本按下 `Ctrl+INSERT` 键。

**粘贴文本**
这取决于你用的是什么`SSH`软件。
`Putty` 要粘贴文本则是点击鼠标右键即可。
`Xshell` 要粘贴文本则是按下 `Shift+INSERT` 键。

**快捷键**
```
^G，Ctrl+G，显示帮助文本
^O，Ctrl+O，保存当前文件
^R，Ctrl+R，读取其他文件并插入光标位置
^Y，Ctrl+Y，跳至上一屏幕
^K，Ctrl+K，剪切当前一行
^C，Ctrl+C，显示光标位置
^X，Ctrl+X，退出编辑文本
^J，Ctrl+J，对其当前段落（以空格为分隔符）
^W，Ctrl+W，搜索文本位置
^V，Ctrl+V，跳至下一屏幕
^U，Ctrl+U，粘贴文本至光标处
^T，Ctrl+T，运行拼写检查
```
