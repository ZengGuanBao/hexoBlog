---
title: mac绑定git中的SSH密匙
tags: [Github]
category: 技术
---
## 步骤1
### 全局修改git的用户名和邮箱
- git config --global user.name "ZengGuanBao" 
- git config --global user.email 672280840@qq.com

### Mac显示隐藏系统文件
- 方法一：（快捷键）
    1. 打开Finder，同时按下三个组合键：Shift + Command + . 
- 方法二：（终端操作，要重启Finder，没方法一快捷）

    1. 显示：defaults write com.apple.finder AppleShowAllFiles -bool true 
    2. 隐藏：defaults write com.apple.finder AppleShowAllFiles -bool false

## 步骤2
###生成密钥
	1.输入指令：ssh-keygen -t rsa -C "672280840@qq.com"，提示输入保存密钥路径，直接回车即可（三次默认回车）。
	2.注：后面是自己的GitHub邮箱
###查看密钥文件
	1.Finder前往：~/.ssh，文件夹内会存在2个文件：id_rsa和id_rsa.pub。
###复制公钥内容
	1. 方法一：Finder打开id_rsa.pub文件，使用文本编辑器打开，复制里面所有文字内容。
	2. 方法二：终端指令复制id_rsa.pub文件内容。
###将公钥内容添加到GitHub
	1. 打开GitHub网站进行登陆；
	2. 到个人设置页Personal Settings；
	3. 找到SSH and GPG keys；
	4. 选择新建SSH key：new ssh key；
	5. 填写和粘贴公钥内容（不含中文）。
