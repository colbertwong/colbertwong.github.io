---
title: hexo下的_post目录下的文件管理
categories:
  - 技术
tags:
  - hexo
date: 2020-02-12 15:15:59
---

### hexo下的_post目录下的文件管理

使用`hexo new <title>`创建新的文章时，文件会被放到`source/_post`目录下，久而久之，文件越积越多，管理起来就会变得很麻烦。可以使用`_config.yml`的`new_post_name`项目来配置创建文件时的目录和文件名。默认值是`:title.md`。我想把每个月的文章放在一个目录下，所以设置值为：`:year/:month/:title.md`。效果如下：

``` yml
# Writing
new_post_name: :year/:month/:title.md # File name of new posts
default_layout: post
```

``` bash
hexo new "hexo下的_post目录下的文件管理"
INFO  Created: D:\work\hexo\source\_posts\2020\02\hexo下的-post目录下的文件管理.md
```

另外，因为我没有安装文章汉字名转拼音的插件，为了避免成的文章的永久链接里出现汉字，所以也修改了`_config.yml`的`permalink`项目的值。

``` yml
permalink: :year/:month/:day-:hour:minute.html
```

``` bash
hexo g
INFO  Start processing
... ...
INFO  Generated: 2020/02/12-1515.html
... ...
```

以上

