---
title: 使用Hexo+Github搭建属于自己的博客
tags: [hexo,Github]
category: 技术
---
工具：Visual Studio Code/MarkdownPad
技术：Hexo+Github

### 创建Github项目

1. Github账户注册和新建项目，项目必须要遵守格式：账户名.github.io，不然接下来会有很多麻烦。并且需要勾选Initialize this repository with a README
2. 在建好的项目右侧有个settings按钮，点击它，向下拉到GitHub Pages，你会看到那边有个网址，访问它，你将会惊奇的发现该项目已经被部署到网络上，能够通过外网来访问它。

### 安装Hexo

1. 在自己认为合适的地方创个文件夹，我是在D盘建了一个blog文件夹。然后在vscode打文件夹
2. 在vscode中打开终端，输入npm install hexo -g，开始安装Hexo
3. 输入hexo -v，检查hexo是否安装成功
4. 输入hexo init，初始化该文件夹（有点漫长的等待。。。）看到后面的“Start blogging with Hexo！”，激动有木有！！！！！
5. 输入npm install，安装所需要的组件
6. 输入hexo g，首次体验Hexo
7. 输入hexo s，开启服务器，访问该网址，正式体验Hexo（假如页面一直无法跳转，那么可能端口被占用了。此时我们ctrl+c停止服务器，接着输入“hexo server -p 端口号”来改变端口号）

### 将本地blog和Github项目联系起来

1. 配置Deployment，在其文件夹中，找到_config.yml文件，修改repository值（在末尾）
2. repository值是你在github项目里的ssh（右下角）
```
deploy:
  type: git
  repository: git@github.com:ZengGuanBao/ZengGuanBao.github.io.git
  branch: master
```

2. 新建一篇博客，在cmd执行命令：hexo new post "博客名"
或者在vscode中新建文件
![](https://i.imgur.com/QEBCOhS.png)

### 把新建的文章更新到Github项目上
1. 在生成以及部署文章之前，需要安装一个扩展：
``` 
npm install hexo-deployer-git --save
```
2. 使用编辑器编好文章，那么就可以使用命令：hexo d -g，生成以及部署了
3. 部署成功后访问你的地址：http://用户名.github.io。那么将看到生成的文章

### 更新主题后，上传没有生效
最后，在查询了一些资料之后，终于知道，这可能是hexo的缓存的问题，也就是你网站根目录的那个db.json文件，还知道了一点，推荐在发布网站之前，先清除缓存，然后再部署网站。 
清除缓存的方法： 
- 执行命令：hexo clean 
- 然后可以生成静态博客并在本地预览：hexo d -g
### 搜索功能

使用站内搜索，安装npm i -S hexo-generator-json-content

### 分享功能

百度分享不支持Https的解决方案

将static文件夹放在网站的根目录下，并将对应的百度分享代码中，把http://bdimg.share.baidu.com/ 改为 /static/api/js/share.js?v=89860593.js?

```
<p><i class="fa fa-share"></i>分享到</p>
<div class="bdsharebuttonbox">
  <a href="#" class="bds_more" data-cmd="more"></a>
  <a href="#" class="bds_fbook" data-cmd="fbook" title="分享到Facebook"></a>
  <a href="#" class="bds_twi" data-cmd="twi" title="分享到Twitter"></a>
  <a href="#" class="bds_linkedin" data-cmd="linkedin" title="分享到linkedin"></a>
  <a href="#" class="bds_qzone" data-cmd="qzone" title="分享到QQ空间"></a>
  <a href="#" class="bds_tsina" data-cmd="tsina" title="分享到新浪微博"></a>
  <a href="#" class="bds_douban" data-cmd="douban" title="分享到豆瓣网"></a>
  <a href="#" class="bds_weixin" data-cmd="weixin" title="分享到微信"></a>
  <a href="#" class="bds_evernotecn" data-cmd="evernotecn" title="分享到印象笔记"></a>
</div>
<script>
  window._bd_share_config = {
	"common": {
	  "bdSnsKey": {},
	  "bdText": "",
	  "bdMini": "2",
	  "bdMiniList": false,
	  "bdPic": "",
	  "bdStyle": "1",
	  "bdSize": "24"
	},
	"share": {},
	"image": {
	  "viewList": ["fbook", "twi", "linkedin", "qzone", "tsina", "douban", "weixin", "evernotecn"],
	  "viewText": "分享到：",
	  "viewSize": "16"
	}
	  };
	  with(document) 0[(getElementsByTagName('head')[0] || body).appendChild(createElement('script')).src =
	'/static/api/js/share.js?v=89860593.js?'];
</script>
```
### 评论功能

评论功能使用的Valine

```
<script src="//cdn1.lncld.net/static/js/3.0.4/av-min.js"></script>
<script src='//unpkg.com/valine/dist/Valine.min.js'></script>
<script>
    new Valine({
        el: '#valine-thread' ,
        notify: ,
        verify: ,
        app_id: '',
        app_key: '',
        placeholder: '',
        pageSize: '',
        avatar: '',
        avatar_cdn:  '',
        visitor: 
    });
</script>
<div id="valine-thread"></div>
```