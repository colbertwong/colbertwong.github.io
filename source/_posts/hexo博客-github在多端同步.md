---
title: hexo博客+github在多端同步
categories:
  - 技术
tags:
  - hexo
  - github
date: 2020-02-11 20:38:51
---

### hexo博客+github在多端同步

在家里的电脑搭好了hexo博客环境之后呢，就想着在公司电脑也可以写呀。于是在github建了个叫`myblog`的新仓库，把博客根目录里的东西一股脑推了上去。嗯？？？一堆乱七八糟的东西被推到了`username.github.io`里去了。不明白啊，先留作业吧，耽误之急是先恢复hexo博客环境，还好有备份（感谢对日开发的职业病）。百度了一圈，赶快memo一下。

- 思路
仓库分两个分支：hexo和master。hexo作为默认分支，存放博客源代码，master分支存放博客生成页面。

- 在github上的`username.github.io`仓库里创建hexo分支，并设置为默认分支。
- 确保本地的博客根目录里有`.gitignore`文件(应该是自动生成的文件)，内容如下：
```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
```
- 进入本地博客根目录，初始化仓库，切换分支，提交文件：
``` bash
git init
git add -A
git commit -m "blog source files"
git branch hexo
git checkout hexo
git remote add origin git@github.com:colbertwong/colbertwong.github.io.git
git push origin hexo // 若发生‘ ! [rejected]        hexo -> hexo (fetch first)’错误，那就强制更新
git push --force origin hexo // 若上一句没有错误，这句可以不用实行
```

- 他终端上的操作（待补充）

