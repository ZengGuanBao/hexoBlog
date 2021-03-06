# Hexo博客

> 使用Hexo+Github搭建的github.io博客

## Hexo搭建步骤
- 安装Git
- 安装Node.js
- 安装Hexo
- GitHub创建个人仓库
- 生成SSH添加到GitHub
- 将hexo部署到GitHub

### 安装Git

> Git是目前世界上最先进的分布式版本控制系统，可以有效、高速的处理从很小到非常大的项目版本管理。也就是用来管理你的hexo博客文章，上传到GitHub的工具。Git非常强大，我觉得建议每个人都去了解一下。廖雪峰老师的Git教程写的非常好，大家可以了解一下。[Git教程](liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

windows：到git官网上下载,Download git,下载后会有一个Git Bash的命令行工具，以后就用这个工具来使用git。

linux：对linux来说实在是太简单了，因为最早的git就是在linux上编写的，只需要一行代码

    sudo apt-get install git

安装好后，用git --version 来查看一下版本

### 安装nodejs

> Hexo是基于nodeJS编写的，所以需要安装一下nodeJs和里面的npm工具。

windows：[nodejs](https://nodejs.org/en/download/)选择LTS版本就行了。

linux：

    sudo apt-get install nodejs
    sudo apt-get install npm

安装完后，打开命令行

    node -v
    npm -v
检查一下有没有安装成功

顺便说一下，windows在git安装完后，就可以直接使用git bash来敲命令行了，不用自带的cmd，cmd有点难用。

### 安装hexo
前面git和nodejs安装好后，就可以安装hexo了，你可以先创建一个文件夹blog，然后cd到这个文件夹下（或者在这个文件夹下直接右键git bash打开）。

输入命令
    
    npm install -g hexo-cli

依旧用hexo -v查看一下版本

至此就全部安装完了。

接下来初始化一下hexo

    hexo init myblog
这个myblog可以自己取什么名字都行，然后

    cd myblog //进入这个myblog文件夹
    npm install
> 新建完成后，指定文件夹目录下有：
- node_modules: 依赖包
- public：存放生成的页面
- scaffolds：生成文章的一些模板
- source：用来存放你的文章
- themes：主题
- ** _config.yml: 博客的配置文件**

安装完成后就可以在本地查看了

    hexo g
    hexo server
打开hexo的服务，在浏览器输入localhost:4000就可以看到你生成的博客了。
使用ctrl+c可以把服务关掉。
### GitHub创建个人仓库
首先，你先要有一个GitHub账户，去注册一个吧。

注册完登录后，在GitHub.com中看到一个New repository，新建仓库


创建一个和你用户名相同的仓库，后面加.github.io，只有这样，将来要部署到GitHub page的时候，才会被识别，也就是xxxx.github.io，其中xxx就是你注册GitHub的用户名。我这里是已经建过了。



点击create repository。

### 生成SSH添加到GitHub

回到你的git bash中，

    git config --global user.name "yourname"
    git config --global user.email "youremail"
这里的yourname输入你的GitHub用户名，youremail输入你GitHub的邮箱。这样GitHub才能知道你是不是对应它的账户。

可以用以下两条，检查一下你有没有输对
    
    git config user.name
    git config user.email
然后创建SSH,一路回车
    
    ssh-keygen -t rsa -C "youremail"
这个时候它会告诉你已经生成了.ssh的文件夹。在你的电脑中找到这个文件夹。
ssh，简单来讲，就是一个秘钥，其中，id_rsa是你这台电脑的私人秘钥，不能给别人看的，id_rsa.pub是公共秘钥，可以随便给别人看。把这个公钥放在GitHub上，这样当你链接GitHub自己的账户时，它就会根据公钥匹配你的私钥，当能够相互匹配时，才能够顺利的通过git上传你的文件到GitHub上。

而后在GitHub的setting中，找到SSH keys的设置选项，点击New SSH key
把你的id_rsa.pub里面的信息复制进去。
在gitbash中，查看是否成功

    ssh -T git@github.com

### 将hexo部署到GitHub

这一步，我们就可以将hexo和GitHub关联起来，也就是将hexo生成的文章部署到GitHub上，打开站点配置文件_config.yml，翻到最后，修改为YourgithubName就是你的GitHub账户

    deploy:
	    type: git
	    repo: https://github.com/YourgithubName/YourgithubName.github.io.git
	    branch: master

这个时候需要先安装deploy-git ，也就是部署的命令,这样你才能用命令部署到GitHub。

    npm install hexo-deployer-git --save

然后

    hexo clean
    hexo generate
    hexo deploy

其中 hexo clean清除了你之前生成的东西，也可以不加。

hexo generate 顾名思义，生成静态文章，可以用 hexo g缩写

hexo deploy 部署文章，可以用hexo d缩写

注意deploy时可能要你输入username和password。

过一会儿就可以在http://yourname.github.io 这个网站看到你的博客了！！


----------

``` bash
# fork克隆本项目后的操作
    npm install
    hexo clean
    hexo generate
    hexo deploy
```
