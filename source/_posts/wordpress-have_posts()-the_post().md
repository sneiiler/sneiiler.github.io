---
title: wordpress - have_posts() the_post()
categories:
  - 计算机
  - 网络
date: 2017-09-24 22:31:27
tags:
---
<!-- more -->
在WordPress的index.php文章循环输出中，通常会有下面一段代码： 
``` php
<?php
if (have_posts()) :
?> 

<?php
while (have_posts()) : the_post();
?>

<?php
endwhile;
?> 

<?php
endif;
?>
```
这里有两个函数，have_posts()和the_post()。 **have_posts()解析：** WordPress的have_posts() 默认是一个全局函数。 have_posts函数被调用时实际上是调用全局变量$wp_query->have_posts()成员函数，来
简单检查一个全局数组（array）变量$posts的一个循环计数器，以确认是否还有post，如果有返回true（1），如果没有返回false（0）。 **the_post()****解析：** the_post()函数则调用$wp_query->the_post()成员函数前移循环计数器，并且创建一个全局变量$post(不是$posts)，把当前的post的所有信息都填进这个$post变量中，以备接下来使用。   简单的使用可以通过函数来直接执行，如the_content()直接显式post的内容，the_title()显式帖子的标题，the_time()显示帖子的时间等WORDPRESS的Template Tags。 高级应用或要定制应用则可以直接调用$post变量的成员。  

* * *

wordpress首页默认是显示所有栏目文章，加入如下粗体部分内容可以只显示id为2,4,5的栏目。 如果只想排除某个栏目，在栏目前添加减号**cat=-3**，表示显示除了id为3的栏目内容   
``` php
<?php
if ( have_posts() ) : 
?> **

<?php
query_posts($query_string . '&cat=2,4,5');
?>** 

<?php
while ( have_posts() ) : the_post(); 
?> 

<?php
get_template_part( 'content', get_post_format() ); 
?> 

<?php
endwhile; 
?> 

<?php
endif; // end have_posts() check 
?>
```