---
title: IE中使用ajax碰到的问题
tags: [hexo,Github]
category: 技术
---
##IE中的crossDomain=true属性设置
再ajax请求过程中设置了crossDomain=true属性，再谷歌内核中是可以正确解读为support.cors = true，发现其他浏览器中都是support.cors = true，唯独在IE中support.cors = false，这个属性的判断来自于support.cors = !!xhrSupported && ( "withCredentials" in xhrSupported )，其中xhrSupported= new window.XMLHttpRequest(),ie9中XMLHttpRequest没有withCredentials属性。也就是说这个问题是由于我的乱用属性加上各浏览器兼容性问题而导致的。
##解决方法

 1. 解决ajax时出现No Transport，在使用ajax之前添加：jQuery.support.cors = true;//浏览器支持跨域访问
 2. 加载jquery-ajaxtransport-xdomainrequest的js
```
<!--[if lte IE 9]><script src="http://cdnjs.cloudflare.com/ajax/libs/jquery-ajaxtransport-xdomainrequest/1.0.3/jquery.xdomainrequest.min.js" type="text/javascript" charset="utf-8"></script><![endif]-->
```
##意外的问题
遇到一个问题就是写的js在客户生产环境中的ie和360中不起作用，随后我想看看浏览器的输出，并没有异常错误，然后继续操作发现一个奇怪的现象就是，在开启F12的情况下，功能正常使用，一旦关闭则使用不了，上网找了资料，参考了superGG1990的文章，在开发过程中，console.log常被用来调试程序，在Chrome和Firefox中友好运行，但是在IE9之前的版本支持不友好，IE6和IE7虽然可以安装 Developer Toolbar，但也不支持console。

> 解决方案：在开发完成过后删除打印的调试信息或者先判断一下js中的console是否存在

```
function log(msg){
    if (window["console"]){
        console.log(msg);
    }
}
```