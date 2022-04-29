---
title: wordpress语言本地化
categories:
  - 计算机
  - 网络
date: 2017-09-24 22:11:42
tags:
---

作为WordPress主题或插件开发者，倡萌建议大家要掌握主题或插件国际化（I18n）/本地化的实现方法。
<!-- more -->
编译函数
----

WordPress使用了下面几个函数来方便语言本地化。

*   `__()`
*   `_e()`
*   `_x()`
*   `_ex()`
*   `_n()`

以上所列的函数是用来包含所需翻译的字符串的，根据字符串的不同参数和输出类型，需要使用不同的函数。相信有不少朋友还是不太明白这几个函数的区别和用法，下面倡萌就来详细说说。

__() 和 _e()
-----------

**__() 和 _e() 都是用来返回对应当前语言的字符串内容**。请看下面的例子： **使用 __()**

``` php
<?php  
if( is_single() ) { //如果这是一篇“文章”  
    echo __( 'This is a post.' );  
}  
?>
```

**使用 _e()**
``` php
<?php  
if( is_single() ) { //如果这是一篇“文章”  
    _e( 'This is a post.' );  
}  
?>
```

上面两组代码的最终输出内容都是一样的。请自己对比一下这两组代码的第 3 行，使用了 echo 函数的，就用 __()，直接返回内容的就用 _e() 。由此，我们可以简单理解为： **如果字符串是返回给其他函数调用，不打印出来，就用 __() ；直接打印输出到 html 中的字符串，就用 _e() 。** 再看下面的例子：
``` php
<?php  
the\_content( \_\_( 'Click here to read more' ) );  
?>
```
‘Click here to read more’ 是被函数 the\_content() 直接包裹的，所以这里使用 \_\_()；如果你换成 \_e() ，它就会直接输出“Click here to read more”，函数 the\_content() 就不起作用了。

\_x() 和 \_ex()
--------------

**如果要翻译的字符串是根据上下文来决定的，就需要用到 _x()。**比如“Post”根据上下文的不同既可以指 “a post_(名词)_” 也可以指 “to post _(动词)_”。你需要**明确表达同一个词的不同含义**，方便翻译者识别。 _x() 主要是用在单个具有多重用法的词语，而且它比其他的编译函数多了一个额外的参数，这个参数就是用来根据不同上下文显示的不同内容。 比如，你在主题的两个地方用到了”post“这个词，但是这两个地方的要表达的意思是不一样的。这时候，你可以这样操作： 在第一处的post使用下面的代码：
``` php
<?php echo _x('post','A post.') ?>
```
在第二处的post使用下面的代码:
``` php
<?php echo _x('post','To post.') ?>
```
那么，翻译者就可以理解两处post的不同，将第一处翻译为“一篇文章”，第二处翻译为“发布”。 注：导出的 .pot 语言包文件，使用 POEdit 软件打开后，你会发现有两条翻译条目分别为：post\[A post\] 和 post\[To post\]，这样就可以分别翻译这两个意思。 **\_ex() 区别于 \_x() 的地方，和 \_e() 区别于\_\_() 是一样的。前者是用于直接打印输出到html的字符串，后者用于返回字符串以供其他函数调用，不打印输出。**

_n()
----

**_n() 是用来进行单复数编译的**。比较常见于 WordPress 的评论功能模块。例如下面的两组代码输出的内容都是一样的：

``` php
<?php  
if(get\_comments\_number() == 1) {  
    _e( 'There is a comment' );  
} else {  
    _e( 'There are comments' );  
}  
?>
```

``` php
<?php  
    echo \_n( 'There is a comment' , 'There are comments' , get\_comments_number() );  
?>
```

第一组代码是通过 if 来判断，如果评论数量是 1 ，就输出“There is a comment ”，否则输出“There are comments”，由于是直接输出的，所以使用 \_e() ；第二组是使用echo 函数输出，然后使用 \_n() 来区分1条评论和多条评论的显示内容。 **_n() 有 3 个参数。第一个是单数形式的字符串，第二个是复数形式的字符串，第三个是引用的数字**。在这个例子中，get\_comments\_number() 是用来获取 评论 的条数，提供给 _n() 使用。

含有变量的翻译
-------

如果在翻译的字符串中包含一个额外的函数或变量，我们应该如何处理呢？比如下面的例子：
``` php
<?php  
    $color = the_color();  
    _e( "You have chosen the $color theme" );  
?>
```
如果你通过 POEdit 制作 .pot 文件，这时会报错。因为在翻译的字符串中包含了 $color 这个变量。那么，如何规避这个问题呢？下面有2种方法：

### 拆分内容
``` php
<?php  
    $color = the_color();  
    echo __( 'You have chosen the ' ) . $color . __( ' theme.' );  
?>
```
仔细看第 3 行代码，使用了 echo 函数，这样就能保证 $color 变量的输出，同时将变量两端的内容分别进行编译，中间使用点号“.”相连。这样一来，只需翻译两端的内容即可。

### 使用 `printf()` 或 `sprintf()`

上面说的“拆分内容”法虽然可以实现我们要的效果，但是它将内容分成几段，需要我们分别翻译，多少有些繁琐。其实我们可以使用 `printf()` 或 `sprintf()` 来解决这个问题。看下面的代码：
``` php
<?php  
    //使用 sprintf() 的写法
    echo sprintf( __( 'You have chosen the %s theme.' ) , the_color() );
 
    //使用 printf() 的写法 
    printf( __( 'You have chosen the %s theme.' ) , the_color() );  
?>
```

你可以看到，翻译的内容中使用了 %s ，而且 翻译的内容 和 变量函数 都被包裹在 `printf()` 或 `sprintf()` 函数中。这个例子中，只使用了一个变量，如果有更多的函数改怎么办？这就需要你自己去了解 `[printf()](http://www.w3school.com.cn/php/func_string_printf.asp)` 或 `[sprintf()](http://www.w3school.com.cn/php/func_string_sprintf.asp)` 这两个函数的了。 **`printf()` 与 `sprintf()` 用法的区别，和 \_e() 与 \_\_() 的区别是一样的。**
