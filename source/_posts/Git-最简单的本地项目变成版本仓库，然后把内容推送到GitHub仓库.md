---
title: Git-最简单的本地项目变成版本仓库，然后把内容推送到GitHub仓库
tags: [Github]
category: 技术
---
工具：Visual Studio Code
技术：Github

###Git-最简单的本地项目变成版本仓库，然后把内容推送到GitHub仓库
（注：本文的前提是本地Git仓库和github仓库之间已经存在SSH key了，所以如果没有建立联系的小伙伴们请先建立联系）

具体操作：

一：把本地项目变成版本仓库
1、把本地的一个项目目录编程版本库repository，例如下图，我把我E盘>A课件>大三2>VUE.JS 变成一个版本库。
> 通过命令 git init 可以吧一个目录变成git管理仓库
![](https://images2015.cnblogs.com/blog/1118105/201703/1118105-20170304200307126-1342942362.png)


2、通过命令git add -A把VUE.JS目录下的所有文件添加到暂存区里面去，git add 可以都很多用法，git add -A只是其中一个，作用是把目录中所有的文件信息添加到索引库的暂存区里面去。注意‘-A’大小写敏感哦，git add -a是失败的哦。
![](https://images2015.cnblogs.com/blog/1118105/201703/1118105-20170304201305032-1750286661.png)

3、通过命令git commit 把刚刚提交到暂存区里的文件提交到仓库。git commit -m "提交所有文件"，-m 后面的文字是注释，方便查看历史记录时知道每一次提交提交的是什么。这一步成功之后，说明本地的项目已经用git版本器管理起来了，接下里就是如何把git本地仓库的内容推送到github仓库去了
![](https://images2015.cnblogs.com/blog/1118105/201703/1118105-20170304201556407-1036188804.png)

二：把本地仓库的内容推送到github仓库去

1、登录github，然后按照下图的步骤Create 一个新的仓库。（博主是个英语渣还好有有道）
![](https://images2015.cnblogs.com/blog/1118105/201703/1118105-20170304202814595-527042763.png)

2、创建完成之后，这时在github上，仓库还是空的，然后我们目前要做的就是把一个已有的本地仓库与github关联，然后，把本地仓库的内容推送到GitHub仓库。


> 我们根据GitHub的提示，在本地的VUE.JS仓库下运行命令，如下图：
		
    git remote add origin https://github.com/SugarTiger/VueTest.git
（红字这个地址是我的，你们填上你们自己的）,然后通过命令git push把本地仓库的内容推送到github仓库去。第一次推送在git push后面加上参数-u，使用-u选项指定一个默认主机。

    $ git push -u origin master
![](https://images2015.cnblogs.com/blog/1118105/201703/1118105-20170305001938954-1976993293.png)
![](https://images2015.cnblogs.com/blog/1118105/201703/1118105-20170305001523532-970373088.png)
3、最后就可以在github上面查看到刚刚push上去的项目内容了
![](https://images2015.cnblogs.com/blog/1118105/201703/1118105-20170305005945391-1878283138.png)

解决每次输入用户名及密码问题
git config --global credential.helper store