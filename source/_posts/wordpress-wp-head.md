---
title: wordpress - wp_head()
categories:
  - 计算机
  - 网络
date: 2017-09-24 21:35:12
tags:
---

<?php //移除顶部多余信息 remove\_action('wp\_head', 'index\_rel\_link');//当前文章的索引 remove\_action('wp\_head', 'feed\_links\_extra', 3);// 额外的feed,例如category, tag页 remove\_action('wp\_head', 'start\_post\_rel\_link', 10, 0);// 开始篇 remove\_action('wp\_head', 'parent\_post\_rel\_link', 10, 0);// 父篇 remove\_action('wp\_head', 'adjacent\_posts\_rel\_link', 10, 0); // 上、下篇. remove\_action('wp\_head', 'adjacent\_posts\_rel\_link\_wp\_head', 10, 0 );//rel=pre remove\_action('wp\_head', 'wp\_shortlink\_wp\_head', 10, 0 );//rel=shortlink remove\_action('wp\_head', 'rel\_canonical' ); wp\_deregister\_script('l10n'); remove\_action('wp\_head','rsd\_link');//移除head中的rel="EditURI" remove\_action('wp\_head','wlwmanifest\_link');//移除head中的rel="wlwmanifest" remove\_action('wp\_head','rsd\_link');//rsd\_link移除XML-RPC remove\_filter('the\_content', 'wptexturize');//禁用半角符号自动转换为全角 remove\_action('wp\_head', array($wp\_widget\_factory->widgets\['WP\_Widget\_Recent\_Comments'\], 'recent\_comments_style'));&nbsp; } ?> 把这段代码插入到主题的functions.php文件下，可以清除WordPress头部大量冗余信息。如有必要，可以看看这些代码的具体意义，以免删除某些你想保留的功能。  

* * *

#### wp_head函数

wp\_head() 是wordpress的一个非常重要的函数，基本上所有的主题在header.php这个文件里都会使用到这个函数，而且很多插件为了在header上加点东西也会用到wp\_head()，比如SEO的相关插件。但是，在wp\_head()出现的这个位置，会增加很多并不常用的代码。可以通过 remove\_action移除这些代码。