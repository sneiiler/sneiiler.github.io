---
title: wordpress - body_class()
categories:
  - 计算机
  - -网络
date: 2017-09-24 21:40:25
tags:
---

wordpress的body_class()函数，顾名思义，这个函数根据不同的页面类型为body标签生成class选择器，从而让设计人员可以各方便灵活的控制不同页面中的各个元素。本文对这一函数进行了详细的解析，包括该函数生成了些什么，所包含的属性值有哪些，以及如何使用和如何新增class选择器等等。   **1、body_class（）生成什么？** body\_class()函数在Wordpress2.7几乎和post\_class()有同样的运行方式，唯一不同的是class生成的名称。 body_class()函数生成的class大多是根据你的访问者在网站的位置。例如，如果访问者在你的博客首页，但你没有设置一个静态主页，函数和类 可能会产生如下所示：

1

`<body ``class``=``"home blog"``>`

生成了两个class类 如果你在某个帖子，body标签看起来可能是这样：

1

`<body ``class``=``"single postid-64"``>`

  如果你正在浏览一个页面，body_class()会生成这样：

1

`<body ``class``=``"page page-id-3 parent-page-id-0 page-template-default"``>`

  从本质上讲，body\_class()会生成基于内容的动态CSS class，以及在什么情况下浏览。例如，如果你是注册用户，且已经登录，body\_class()会在body标签生成一个登录class。 以下为可用的body class的完整列表：

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

`rtl`

`home`

`blog`

`archive`

`date`

`search`

`paged`

`attachment`

`error404`

`single postid-(id)`

`attachmentid-(id)`

`attachment-(mime-type)`

`author`

`author-(user_nicename)`

`category`

`category-(slug)`

`tag`

`tag-(slug)`

`page`

`page-parent`

`page-child parent-pageid-(id)`

`page-template page-template-(template file name)`

`search-results`

`search-no-results`

`logged-``in`

`paged-(page number)`

`single-paged-(page number)`

`page-paged-(page number)`

`category-paged-(page number)`

`tag-paged-(page number)`

`date-paged-(page number)`

`author-paged-(page number)`

`search-paged-(page number)`

  **2\. 如何添加body_class()** 假设你正在使用Wordpress2.8以上的版本，通常body_class()放到<body>标签里。它通常在header.php文件里。 当你找到标签的位置后，请把它更改为：

1

`<body <?php body_class(); ?>>`

  **3\. 使用动态Body Class** 现在我们有了body class，有什么大不了呢？我将会解释： 除了html元素外，标签包围着其他所有的HTML代码。因此，body class允许我们对网页任何元素进行修改，具体到当前页面。 也许通过实例更容易理解： 我们主题左边有一个<div id=”content”>，右边有一个<div id=”sidebar”>，他们都在一个960px宽<div id=”container”>里。content div为600px宽，sidebar div为360px宽。但是，当浏览单独的帖子页面，我让我的主题不显示sidebar。现在，我们只剩下一个content div。不幸的是，container div为960px宽，而我们的content div却只有600px宽。 我们难道用一个大空白区填充我们的工具栏？该如何解决呢？使用body class这将很简单。我们只需要针对<div id=”content”>在帖子页的情况进行定义。在CSS里为：

1

`.single #content{ width: 960px; }`

通过这样做，在帖子页面，content div为960px宽。我们正在增加一个简单有选择性的CSS系统。   **4\. 新增body_class()的class** 在某些情况下，你将要添加自己的Class到body\_class()里。如果你发现自己处在这种情况下，这些有些方法可以做到这一点。 首先，最简单的方法是通过自定义Class函数调用 body\_class()

1

`<body <?php body_class(``'my-class'``); ?>>`

通过这样做，我们现在告诉body\_class()函数增加my-class的输出。 第二，困难但更灵活的方式是，利用Wordpress的过滤器，增加新的body class。在这种情况下，我们将使用 get\_body\_class() 函数中的body\_class过滤器。 这是增加使用过滤器增加class的例子：

1

2

3

4

5

6

7

8

9

10

11

`<?php`

`add_filter(’body_class’,'my_body_classes’);`

`function my_body_classes($classes) {`

`// add 'zdy_class' to the $classes array`

`$classes[] = ``'zdy_class'``;`

`// return the $classes array`

`return` `$classes;`

`}`

`?>`

则输出结果在body\_class()的基础上新增zdy\_class  

* * *

body_class 函数是什么？用来做什么？
-----------------------

有一定前端开发经验的人，往往会在 body 标签上加上一些类，变成类似下面这样：

    <body class="home">.....</body>

因为同一个网站中，很多页面的结构是相同的，但是有时某个相同结构（.header）的样式却要求不同。这样如果使用相同的结构，就没法修改样式，如果再新建结构，就相当于重做了一个页面，增加工作量。这时，也可以在 body 标签上加上一个页面对应的类（blog），之后对于这样一个与其他页面不同样式的需求，就可以使用下面语句来实现：

    .blog .header{.....}

body_class 这个函数就是用来给 body 标签添加类的函数。

body_class 函数如何使用？
------------------

body_class 函数的使用方法非常简单，只需要用下面语句替换掉原来的 body 标签即可：

    <body <?php body_class($class); ?>>

其中有一个参数 class ，它可以是一个字符串或者是数组，数组里的内容会以空格为分割，插入到 body 标签中的 class 属性中。

body_class 函数会输出什么类？
--------------------

既然它会自动的输出类让前端方便进行控制，那么了解这个函数的输出规则就非常有必要了，下面针对不同类型的页面介绍一下它的输出规则：

### 首页（Front Page）

这里的首页，就是打开你的博客看到的第一个页面，这个页面是可以在 WordPress 后台进行设置的，可以选择显示文章列表或者是一个静态的页面（Page）。 任意的首页都包含 `home` 类。

*   如果网站首页显示文章列表，那么输出：`home blog` 这两个类。
*   如果网站首页显示静态页面，将会输出：`home page` 类。

### 博客文章索引页面

博客文章索引页面都包含 `blog` 类。

*   如果博客文章页面显示在首页，将会输出：`home blog` 类。
*   如果博客文章显示在某个指定的静态页面中，将会输出：`page blog` 类。

### 文章页面（Single Post）

所有的文章都会输出：`single postid-{ID}` 这两个类（ID 为当前文章唯一的 ID ）。

*   普通的文章页面输出：`single-post` 类
*   自定义文章类型的文章页面输出：`single-{posttype}` 类
*   如果支持文章格式的话：
    *   指定了文章格式的文章会输出：`single-format-{format}`
    *   如果当前文章没有指定文章格式：`single-format-standard`
*   对于附件页面（attachment pages）会输出：`attachment single-attachment attachmentid-{ID} attachment-mime-type`

### 存档页面（Archives）

存档页面都有 `archive` 类。

*   日期（Date）存档索引页面输出：`date`
*   自定义文章类型的存档索引页面输出：`post-type-archive post-type-archive-{posttype}`
*   作者存档页面输出：`archive author author-{user_nickname}`
*   标签存档页面输出：`archive tag tag-{slug}`
*   分类存档页面输出：`archive category category-{slug}`
*   自定义分类（Taxonomy）存档页面输出：`tax-{taxonomy} term-{term} term-{ID}`
*   自定义文章格式存档页面输出：`tax-{post_format} term-post-format-{format} term-{ID}`

### 页面（Page）

所有静态页面都输出 `page` 和 `page-id-{ID}` 类。 页面层次中：

*   父级页面输出：`page-parent`
*   子级页面输出：`page-child parent-pageid-{ID}`

[自定义页面模版](http://blog.wpjam.com/m/custom-wordpress-page-template/)中：

*   应用了页面模版的页面会输出：`page-template page-template-{directory}{filename}_php`
*   没有指定页面模版的页面会输出：`page-template-default`

### 搜索页面

搜索结果页面都有 `search` 类。

*   带有结果的搜索页面：`search-results`
*   没有结果的搜索页面：`search-no-results`

### 分页页面或者多页码的页面

分页页面通常是指文章索引页面底部的翻页。 此外文章内也有分页页面。一个页面或者文章太长的时候，通常会截断成多个子页面，通过翻页查看下一部份内容。对于所有带有页码的页面，都包含 paged 类。当前页面处于某个带有页码页面的第二页之后的页面，会输出 paged 和 paged-{n} 类。

*   文章带页码页面：`single-paged-{n}`
*   静态页面带页码：`page-paged-{n}`
*   分类存档索引页面：`category-paged-{n}`
*   标签存档索引页面：`tag-paged-{n}`
*   日期存档索引页面：`date-paged-{n}`
*   作者存档索引页面：`author-paged-{n}`
*   搜索结果页面：`search-paged-{n}`
*   自定义文章类型索引页面：`post-type-paged-{n}`

### 404 错误页面

错误页面输出 `error404` 类。

### 登陆

当用户登陆 WordPress 之后，会在所有页面输出 `logged-in` 类。

### 文字方向

如果文字的方向设置为了 “右向左” 就会输出 `rtl` 类。

### 自定义背景

如果使用了自定义背景功能来显示背景图片或者颜色，会输出 `custom-background` 类。

### 超级管理员工具条

如果管理员工具条在顶部出现了，会输出： `admin-bar no-customize-support` 类。 介绍完了 body_class 函数根据当前页面自动输出类的规则之后，我们来介绍一下如何自定义输出的类。

自定义 body_class 函数输出的类
---------------------

在前面的使用中已经提到了这个函数的唯一的参数，传递进去值就会输出相应的参数，这里不再赘述。下面介绍一下通过条件判断和过滤器自定义输出类。 通过使用 body_class filter 来实现，大体框架如下：

    add_filter('body_class','wpjam_class_names');
    function wpjam_class_names($classes) {
    	$classes[] = 'class-name';
    	return $classes;
    }

上例中，我们为 classes 这个数组变量增加了一个新键值 “class-name” 并返回给 body_class filter ，即可实现在所有页面中输出 “class-name” 这个类。 但是这样自定义是完全没有什么价值的，我们往往希望通过更详细的判断语句来判断出某些特定的页面，然后增加相应的类。这样，就需要 WordPress 强大的条件判断标签了。这里推荐一下 [我爱水煮鱼](http://blog.wpjam.com/) 博客翻译编写的 [WordPress 条件判断标签及其使用方法](http://blog.wpjam.com/article/wordpress-conditional-tags/)。下面就来试一下：

    add_filter('body_class','wpjam_class_names');
    function wpjam_class_names($classes) {
    	if ( is_page( 'some-page' ))
    		$classes[] = 'some-page';
    	return $classes;
    }

上面例子很简单，使用 is\_page 判断标签判断当前页面的 slug 是否为 some-page ，如果是，就为当前页面的 body 标签增加 some-page 类。当然，因为默认输出的已经比较详细了，所以这个例子只作为抛砖引玉之用。 需要注意一点，WordPress 系统在不断的升级，可能会对本文中的输出类的规则有所变更，如果你发现某个规则是错误的，请以实际输出为准。 总之 body\_class 差不多就这么些事情，使用它可以方便前端工作，提高灵活性。所以，为了你的主题更具有扩展性，务必要在 body 标签中加入这个函数哦！

标签：[WordPress 教程](http://blog.wpjam.com/tag/wordpres-tutorials/)

©我爱水煮鱼