---
title: 安装 Git
tags: [Github]
category: 技术
---
# 安装 Git #
- 在 Mac 上安装
- 在 Mac 上安装 Git 有多种方式。 最简单的方法是安装 Xcode Command Line Tools。 Mavericks （10.9） 或更高版本的系统中，在 Terminal 里尝试首次运行 git 命令即可。 如果没有安装过命令行开发者工具，将会提示你安装。

- 如果你想安装更新的版本，可以使用二进制安装程序。 官方维护的 OSX Git 安装程序可以在 Git 官方网站下载，网址为 [http://git-scm.com/download/mac。](http://git-scm.com/download/mac)

- 在 Windows 上安装
- 简单的方法是安装 GitHub for Windows。 该安装程序包含图形化和命令行版本的 Git。 它也能支持 Powershell，提供了稳定的凭证缓存和健全的 CRLF 设置。 稍后我们会对这方面有更多了解，现在只要一句话就够了，这些都是你所需要的。 你可以在 GitHub for Windows 网站下载，网址为 [https://git-for-windows.github.io](https://git-for-windows.github.io)。

# Git 版本管理 # 
- 经验：本地登录SSH认证

- 首先进行本地SSH公钥的生成。打开git bash终端，键入：**SSH-KEYGEN -T RSA -C "邮箱地址"**
这里的邮箱地址即为你的github账号邮箱。

1. 执行前述命令后若成功则会提示在用户文件夹下生成了ssh公钥的文件。
是否成功可以通过访问文件夹 .ssh 来确定，若有此文件夹则说明生成成功。

2. 在资源管理器中打开这个.ssh文件夹，在它下面会看到两个文件，
选择后缀名为.pub的文件并用记事本打开，复制这个文件中的所有内容。

3. 打开浏览器登陆github，在自己的账户面板下找到
SSH keys这一栏，打开后即会看到目前该账户下已进行过SSH认证的机器，
选择Add SSH key之后，将前一步复制的内容粘贴至Key中，同时需要编辑一个Title来说明此Key认证的是哪一台机器，通常会使用计算机的名字。

4. 保存后，回到git bash中，
键入 ssh git@github.com进行连接认证，
其中有一步会询问是否确定进行连接，需要键入yes。
若认证成功后将会有如图所示的返回结果字样。

5. 在完成认证后，即可将git上的开源项目或自己账号下的私有项目clone到本地。
