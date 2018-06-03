---
title: wordpress - is_home()
categories:
  - 计算机
  - 网络
date: 2017-09-24 22:27:17
tags:
---

is_home()判断是否为首页。如果不起作用，大致有如下两个常见原因： **第一种：** 当你的首页不是默认的index.php的时候，而是在后台指定了一个page页面。这种情况下is\_home()会失效，也就是说这样子的情况下就不能再用is\_home()来判断。 is\_front\_page()是判断当前页是不是指定的首页，我们在上面描述的情况下需要的就是这个函数。

<?php if (is_home() || is\_front\_page()) { ?>
我只会在首页显示
<?php } ?>

ps：我在使用多站点wordpress进行二次开发时，需要所有的站点均指定一个page作为首页来显示；而且，该page作为首页显示时，页头还要显示一个banner图片。这就需要对所有theme主题的page.php文件内使用上述代码以判断是否首页。 **第二种：** 如果is\_home()之前有个 query\_posts()，则会让它本身判断失效。原因是 is\_home() 函数在首页的时候会返回一个 true 来判断，而 query\_posts()会阻断这一判断。 解决方案是在 is\_home()之前加一个 wp\_reset_query()。

<?php wp\_reset\_query(); if ( is_home() ) { ?> 
我只会在首页显示
<?php } ?>