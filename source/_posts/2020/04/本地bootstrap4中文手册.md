---
title: 本地bootstrap4中文手册
categories:
  - 技术
tags:
  - 前端
  - bootstrap4
date: 2020-04-08 10:51:03
---

## 本地bootstrap4中文手册

今天有同事来问我，能不能帮忙找个`bootstrap4`的离线手册。因为之前下载过`bootstrap3`的离线手册并收藏了[网址](https://www.bootcss.com/)，就满口答应了下来。结果尴尬了，该网站并不提供`bootstrap4`的离线手册，只有在线的。于是继续搜索，更尴尬的事情发生了，没找到。。。由于信息安全的要求，整个部门都是离线开发的，所以离线手册对我们来讲挺重要的。小学生守则教导我们，答应别人的事情要努力做到(其实是不能跌份儿啊)。于是曲线救国，在`github`上找到了`bootstrap4`的[中文手册翻译项目](https://github.com/tmplink/bootstrap4_chinese)，读了一下readme，是支持在本地用一个web服务器让它跑起来的。

下载工程，传到内网web服务器，解压，子目录方式访问（http://localhost/bootstrap4cn/）,嗯？一片空白？赶快开发者模式看一下，访问`index.html`时，`http://localhost/config/pre.html?v=1586316257938`找不到。url中缺少了子目录，调查了一下，该项目试用了一个叫`domloader.js`的前端加载小工具，如果需要使用子目录方式访问的话，需要设置一个`domloader.root`的参数[参考文章《HTML模板加载对象，简化并优化前端开发的小工具domloader》](https://www.anspoon.com/domloader-3444.html)。`config/init.html`和`js/domloader.js`里都有`domloader.root`,值全部修改为`http://localhost/bootstrap4cn/`（其实只修改init.html里的即可），再次访问（http://localhost/bootstrap4cn/），成功访问首页。高兴的点击一下【让我们开始吧】按钮，嗯？又来？一片空白？继续调查，访问`http://localhost/bootstrap4cn/pages/getting_started.html`页面时，`http://localhost/config/pre.html?v=1586325297234`找不到。已经改过`domloader.root`了啊，怎么还有这种问题呢。打开`pages/getting_started.html`文件，发现代码`domloader.preload('../config/pre.html');`。和`init.html`里的root值一结合，嗯，完美干掉了的子目录`bootstrap4cn`。直接修改`domloader.preload('../config/pre.html');`为`domloader.preload('config/pre.html');`。刷新浏览器，开始页面也出来了。一顿展开，`pages`目录下的文件都做相同的修改。随意进入了几个页面，好像没有其他问题了。

如果不使用子目录方式访问的话，是不需要做任何修改的。

以上
