---
title: WordPress函数query_posts用法汇总
categories:
  - 计算机
  - 网络
date: 2017-09-24 22:33:41
tags:
---

最近经常有网友跟我咨询WordPress函数query\_posts的相关用法，说起来query\_posts实在是太强大，参数无数，用法更是无数，如果让我说它的用法，我根本没法一一说清楚。开始之前，你可以先看看[query_posts的官方文档](https://www.ludou.org/go/wl-aHR0cDovL2NvZGV4LndvcmRwcmVzcy5vcmcvRnVuY3Rpb25fUmVmZXJlbmNlL3F1ZXJ5X3Bvc3Rz "query_posts官方文档")，query_posts的全部参数可以参考：[WP_Query](https://www.ludou.org/go/wl-aHR0cDovL2NvZGV4LndvcmRwcmVzcy5vcmcvQ2xhc3NfUmVmZXJlbmNlL1dQX1F1ZXJ5 "WP_Query")。不过看文档对很多人来说可能会很困难，本文将介绍几种常见的用法，不过一切用法都是从官方文档中来的，学会看文档才是王道。 query\_posts函数在WordPress主题中是用于控制哪些文章可以出现在主循环中，可能说主循环很多人都不懂，那么举个例子，首页、存档页的这些文章（包括分页中的）都是在主循环中的。在不使用query\_posts函数控制的情况，首页、存档页等都是按照文章的发布时间列出你博客上所有已发布的文章，而如果你想定义哪些文章可以显示，哪些文章不显示，文章按照什么样的方法排序等，那么你就要用到query\_posts函数了，本站首页的文章排序：随机阅读、评论最多和标题排序就是用query\_posts函数来实现的。

### 基本用法：

首先介绍一下如何使用query_posts函数。在主题目录下找到存档页面文件，存档页面包括index.php、archive.php等，一般分类页、标签页、日期页和作者页等都是用archive.php，具体的WordPress主题文件构成可以看这篇文章：[WordPress主题文件构成](https://www.ludou.org/create-wordpress-themes-template-hierarchy.html "WordPress主题制作全过程（二）：主题文件构成") 确定了你要控制哪个页面的文章列表，那么我们就可以开始了，比如你想让首页的文章按评论数排序，那么index.php中的代码基本框架就是这样的：
``` php
<?php

    // query_posts函数
    query_posts('orderby=comment_count');

    // 主循环
    if ( have_posts() ) : while ( have_posts() ) : the_post();
        ..
    endwhile; else:
        ..
    endif;

    // 重置query
    wp_reset_query();

?>
```
其实你要做的就是在index.php中查找`if (have_posts())`或`while (have_posts())`，在前面添加query\_posts函数即可。不过以上方式可能会导致首页无法分页，那你可以将query\_posts函数改成这样的行式：
``` php
$args = array(
    // query_posts参数，具体参数可以参加官方文档
    'orderby'   => comment_count
);

// 下面这一行代码是必须的，不然不能分页
$arms = array_merge($args, $wp_query->query);
query_posts($arms);
```
下面是一些常见的query_posts函数用法，你可以直接用到你的主题中。

### 一、只显示含有某个自定义字段的文章

如果你想只显示添加了某个自定义字段的文章，并按照这个字段的值来对文章排序，那么你可以参加这篇文章：[WordPress手动修改文章排列顺序](https://www.ludou.org/wordpress-customize-posts-order.html "WordPress手动修改文章排列顺序") 其实这种方式你可以看成怎样只显示我推荐的文章，那么含有这个自定义字段的文章就是推荐文章。

### 二、怎样让某分类的文章不显示/显示

如果你不想让某分类的文章出现在主循环中，那么你可以使用query\_posts添加参数category\_\_not_in即可：
``` php
$paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
$args = array(
    // 2, 6就是你不想显示的分类ID，多个用半角逗号隔开
    'category__not_in'   => array(2, 6),
    'paged' => $paged
);
query_posts($args);
```
如果只想让显示某个分类的文章，可以将category\_\_not\_in改成category\_\_in。同理，如果不显示某标签下的文章，可以将category\_\_not\_in改成：tag\_\_not\_in，或者只想让显示某个标签下的文章，可以将category\_\_not\_in改成tag\_\_in，后面跟着标签的ID即可。

### 三、如何对文章进行排序
``` php
$paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
$args = array(
    // 以下代码中的title就是orderby的值，按标题排序
    'orderby'   => title,
    'paged' => $paged
);
query_posts($args);
```
根据orderby的值不同，可以让文章按照很多种方式进行排序，下面是列举几个常见的值及其对应的排序方式:title：按标题；date：按发布日期；modified：按修改时间；ID：按文章ID；rand：随机排序；comment_count：按评论数

### 四、只显示相应ID的文章

如我只想显示ID为2,4,6的文章，可以使用以下代码：
``` php
$paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
$args = array(
    // 以下代码中的2,4,6就是文章的ID
    'post__in'   => array(2,4,6),
    'paged' => $paged
);
query_posts($args);
```
如果不想显示2,4,6这几篇文章，可以将 post\_\_in 改成 post\_\_not_in 。另外如果只想显示置顶文章，那么可以将array(2,4,6)改成`get_option('sticky_posts')`，这段代码会自动给你填充所有置顶文章的ID。

### 五、让置顶文章不置顶

如果你不想让置顶文章显示在顶部，而是让它们安装正常的顺序排列，那么可以使用以下代码：
``` php
$paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
$args=array(
    'paged' => $paged,
    'ignore_sticky_posts' => 1
);
query_posts($args);
```
### 六、列出所有状态的文章

WordPress的文章状态有很多种，包括已发布、草稿、已删除、私人的、定时发布的等等，如果你想将这些文章都统统显示出来，那么可以这样：
``` php
$paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
$args = array(
    'post_status' => array('publish', 'pending', 'draft', 'future', 'private', 'trash'),
    'paged' => $paged
);
query_posts($args);
```
post_status参数可以控制具体的文章状态，值包括pending（待审）、publish（已发布）、draft（草稿）, future（定时）, private（私有）, trash（已删除）。

### 七、控制文章的数量

如果你想控制要显示的文章数量，可以使用showposts参数：
``` php
$paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
$args = array(
    // 控制只显示10篇文章，如果将10改成-1将显示所有文章
    'posts_per_page' => 10,
    'paged' => $paged
);
query_posts($args);
```
如果你只是想控制首页、分类页等每各分页显示的文章数量，可以在WordPress管理后台 - 设置 - 阅读那里设置博客页面至多显示多少篇文章。 -- 完 --