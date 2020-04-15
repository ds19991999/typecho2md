# Windows 开启 sshd 服务

现在的`windows 10`版本默认自带`openssh`服务，可以直接用，在`设置–>应用和功能–>管理可选功能`选择`openssh`安装就可以了。

## 配置

打开`powershell`

```powershell
# 检查一下 openssh 的安装
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'
```

![](https://image.creat.kim/20190615174445.png)

```powershell
# 使用 PowerShell 安装服务器
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

![](https://image.creat.kim/20190615174556.png)

安装完成之后，就需要进行一些初始化配置了，还是以管理员身份，使用 `PowerShell` 执行即可。

```
# 开启 SSHD 服务
Start-Service sshd
# 设置服务的自动启动
Set-Service -Name sshd -StartupType 'Automatic'
# 确认一下防火墙是否是放开的
Get-NetFirewallRule -Name *ssh*
```

如果是放开的，那么结果会提示 `OpenSSH-Server-In-TCP`这个状态是 `enabled`。

![](https://image.creat.kim/20190615174926.png)

## 登录

与`linux`登录一样，用另外一台机子输入`ssh usernaame@ip`，然后输入密码就可以进行远程登陆到`win`的`CMD`

