---
title: WordPress主题制作全过程（二）：主题文件构成
categories:
  - 计算机
  - 网络
date: 2017-09-24 22:35:16
tags:
---
<!-- more -->
在开始制作WordPress主题之前，首先得了解WordPress主题到底由哪些文件构成，你得清楚WordPress程序是怎样与主题文件连接的。 以下是WordPress默认主题default文件夹下的所有模板文件。看了下图，可能你还摸不着头脑，到底这些文件是干什么的。WordPress的主题是用[PHP](https://www.ludou.org/go/wl-aHR0cDovL3poLndpa2lwZWRpYS5vcmcvemgtY24vUEhQ)编写的，而不是纯HTML + CSS，所以模板文件的后缀名是.php，如果你想精通WordPress的主题制作，完美控制你的博客，最好要熟悉[PHP](https://www.ludou.org/go/wl-aHR0cDovL3poLndpa2lwZWRpYS5vcmcvemgtY24vUEhQ)编程。要是不会[PHP](https://www.ludou.org/go/wl-aHR0cDovL3poLndpa2lwZWRpYS5vcmcvemgtY24vUEhQ)编程怎么办？就做不了WordPress主题了吗？那也不是，至少看完本系列教程，你也能够掌握基本的WordPress主题制作方法。 ![WordPress主题文件构成](https://up.ludou.org/blog/wp-content/uploads/2010/04/themefile.jpg "WordPress主题文件构成") 下面是WordPress主题文件层次结构，它会告诉你：当WordPress显示特定的页面类型时，会使用哪个模板文件呢？只有了解了以下主题层次结构，你才能知道你的WordPress主题到底需要写哪些文件。

### 怎么看下面的文件层次结构？

以主页为例，下面有2个文件home.php和index.php，WordPress程序会从你的主题文件夹中依次查找这两个文件：

*   如果找到home.php，则使用home.php作为博客首页模板，即使你的主题文件夹中有index.php；
*   如果home.php未找到，则使用index.php作为首页模板；
*   如果home.php和index.php都找不到，你的主题将不会被WordPress识别，等于废物。

### 主页

1.  home.php
2.  index.php

**文章页：**

1.  single-{post_type}.php - 如果文章类型是videos（即视频），WordPress就会去查找single-videos.php（WordPress 3.0及以上版本支持）
2.  single.php
3.  index.php

### 页面

1.  自定义模板 \- 在WordPress后台创建页面的地方，右侧边栏可以选择页面的自定义模板
2.  page-{slug}.php - 如果页面的缩略名是news，WordPress将会查找 page-news.php（WordPress 2.9及以上版本支持）
3.  page-{id}.php - 如果页面ID是6，WordPress将会查找page-6.php
4.  page.php
5.  index.php

### 分类

1.  category-{slug}.php - 如果分类的缩略名为news，WordPress将会查找category-news.php(WordPress 2.9及以上版本支持)
2.  category-{id}.php -如果分类ID为6，WordPress将会查找category-6.php
3.  category.php
4.  archive.php
5.  index.php

### 标签

1.  tag-{slug}.php - 如果标签缩略名为sometag，WordPress将会查找tag-sometag.php
2.  tag-{id}.php - 如果标签ID为6，WordPress将会查找tag-6.php（WordPress 2.9及以上版本支持）
3.  tag.php
4.  archive.php
5.  index.php

### 作者

1.  author-{nicename}.php - 如果作者的昵称为rami，WordPress将会查找author-rami.php（WordPress 3.0及以上版本支持）
2.  author-{id}.php - 如果作者ID为6，WordPress将会查找author-6.php（WordPress 3.0及以上版本支持）
3.  author.php
4.  archive.php
5.  index.php

### 日期页面

1.  date.php
2.  archive.php
3.  index.php

### 搜索结果

1.  search.php
2.  index.php

### 404 (未找到)页面

1.  404.php
2.  index.php

### 附件页面

1.  MIME_type.php - 可以是任何MIME类型 (image.php, video.php, audio.php, application.php 或者其他).
2.  attachment.php
3.  single.php
4.  index.php

  ![](https://developer.wordpress.org/files/2014/10/wp-hierarchy.png)