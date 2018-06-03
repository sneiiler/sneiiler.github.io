---
title: wordpress - get_header()
categories:
  - 计算机
  - 网络
date: 2017-09-24 22:18:54
tags:
---

描述
--

从当前主题中引入 header.php 模板文件。如果名字是特定的，那么包含特定名称的头部文件 header-{name}.php 就会被引入。 如果主题没有 header.php 文件，就会引入默认文件 `wp-includes/theme-compat/header.php` 。

用法
--
``` php

<?php
get_header( $name );
?>
```
参数
--

$name

(_string_) (_可选_) 调用 header-name.php.

默认: _None_

例子
--

### 简单的 404 页面

下面的代码是一个简单模板文件，专门用来显示 "HTTP 404: Not Found" 错误的 （这个文件应该包含在你的主题中，名为 404.php）
``` php
<?php
get_header();
?>
<h2>Error 404 - Not Found</h2>
<?php
get_sidebar();
?>
<?php
get_footer();
?>
```
### 多种头部

为不同的页面显示不同的头部
``` php
<?php
if ( is_home() ) :
	get_header( 'home' );
elseif ( is_404() ) :
	get_header( '404' );
else :
	get_header();
endif;
?>
```
这些为 home 和 404 准备的头部应该分别命名为  header-home.php 和 header-404.php 。

资源文件
----

get_header() 包含在 `wp-includes/general-template.php`.

相关函数
----

get_footer(), get_sidebar(), get_template_part(), get_search_form(),comments_template()