---
title: wordpress - bloginfo()
categories:
  - 计算机
  - 网络
date: 2017-09-24 23:01:02
tags:
---

bloginfo( string $show = '' )
=============================

显示当前网站的信息。
<!-- more -->
具体参数如下：

### Possible values for $show [#Possible values for $show](https://developer.wordpress.org/reference/functions/bloginfo/#possible-values-for-show)

 

*   ‘**name**‘ – Displays the “Site Title” set in Settings > General. This data is retrieved from the “blogname” record in the [wp_options table](https://codex.wordpress.org/Database_Description#Table:_wp_options "Database Description").
*   ‘**name**‘ – 显示在网站后台设置的 网站标题
*   ‘**description**‘ – Displays the “Tagline” set in Settings > General. This data is retrieved from the “blogdescription” record in the [wp_options table](https://codex.wordpress.org/Database_Description#Table:_wp_options "Database Description").
*   ‘**description**‘ – 显示网站后台中设置的  网站描述
*   ‘**wpurl**‘ – Displays the “WordPress address (URL)” set in Settings > General. This data is retrieved from the “siteurl” record in the [wp_options table](https://codex.wordpress.org/Database_Description#Table:_wp_options "Database Description"). Consider echoing [site_url()](https://developer.wordpress.org/reference/functions/site_url/) instead, especially for multi-site configurations using paths instead of subdomains (it will return the root site not the current sub-site).
*   ‘**wpurl**‘ - 显示wordpress网站的 根网址，建议使用输出site_url()函数来输出，尤其是对于多站点配置的网站
*   ‘**url**‘ – Displays the “Site address (URL)” set in Settings > General. This data is retrieved from the “home” record in the [wp_options table](https://codex.wordpress.org/Database_Description#Table:_wp_options "Database Description"). Consider echoing [home_url()](https://developer.wordpress.org/reference/functions/home_url/) instead.
*   ‘**url**‘ - 显示当前网站的网址，建议使用home_url()函数来代替
*   ‘**admin_email**‘ – Displays the “E-mail address” set in Settings > General. This data is retrieved from the “admin_email” record in the [wp_options table](https://codex.wordpress.org/Database_Description#Table:_wp_options "Database Description").
*   显示网站管理员的邮箱
*   ‘**charset**‘ – Displays the “Encoding for pages and feeds” set in Settings > Reading. This data is retrieved from the “blog_charset” record in the [wp_options table](https://codex.wordpress.org/Database_Description#Table:_wp_options "Database Description"). **Note:** this parameter always echoes “UTF-8”, which is the default encoding of WordPress.
*   输出网站的默认编码
*   ‘**version**‘ – Displays the WordPress Version you use. This data is retrieved from the $wp_version variable set in `wp-includes/version.php`.
*   输出wordpress的版本号
*   ‘**html_type**‘ – Displays the Content-Type of WordPress HTML pages (default: “text/html”). This data is retrieved from the “html_type” record in the [wp_options table](https://codex.wordpress.org/Database_Description#Table:_wp_options "Database Description"). Themes and plugins can override the default value using the [pre\_option\_html_type](https://developer.wordpress.org/reference/hooks/pre_option_option/ "Plugin API/Filter Reference") filter.
*   输出Content-Type
*   ‘**text_direction**‘ – Displays the Text Direction of WordPress HTML pages. Consider using [is_rtl()](https://developer.wordpress.org/reference/functions/is_rtl/) instead.
*   输出网站是从左到右还是从右到左显示顺序
*   ‘**language**‘ – Displays the language of WordPress.
*   显示wordpress使用的语言
*   ‘**stylesheet_url**‘ – Displays the primary CSS (usually _style.css_) file URL of the active theme. Consider echoing [get\_stylesheet\_uri()](https://developer.wordpress.org/reference/functions/get_stylesheet_uri/) instead.
*   显示当前使用主题的样式文件 style.css 的网址，可以使用 get\_stylesheet\_uri()函数
*   ‘**stylesheet_directory**‘ – Displays the stylesheet directory URL of the active theme. (Was a local path in earlier WordPress versions.) Consider echoing [get\_stylesheet\_directory_uri()](https://developer.wordpress.org/reference/functions/get_stylesheet_directory_uri/) instead.
*   ‘**template_url**‘ / ‘**template_directory**‘ – URL of the active theme’s directory. Within child themes, both get\_bloginfo(‘template\_url’) and [get_template()](https://developer.wordpress.org/reference/functions/get_template/) will return the _parent_ theme directory. Consider echoing [get\_template\_directory_uri()](https://developer.wordpress.org/reference/functions/get_template_directory_uri/) instead (for the parent template directory) or [get\_stylesheet\_directory_uri()](https://developer.wordpress.org/reference/functions/get_stylesheet_directory_uri/) (for the child template directory).
*   输出当前网站模板的uri
*   ‘**pingback_url**‘ – Displays the Pingback XML-RPC file URL (_xmlrpc.php_).
*   ‘**atom_url**‘ – Displays the Atom feed URL (_/feed/atom_).
*   ‘**rdf_url**‘ – Displays the RDF/RSS 1.0 feed URL (_/feed/rfd_).
*   ‘**rss_url**‘ – Displays the RSS 0.92 feed URL (_/feed/rss_).
*   ‘**rss2_url**‘ – Displays the RSS 2.0 feed URL (_/feed_).
*   ‘**comments\_atom\_url**‘ – Displays the comments Atom feed URL (_/comments/feed_).
*   ‘**comments\_rss2\_url**‘ – Displays the comments RSS 2.0 feed URL (_/comments/feed_).
*   ‘**siteurl**‘ – Deprecated since version 2.2. Echo [home_url()](https://developer.wordpress.org/reference/functions/home_url/), or use bloginfo(‘url’).
*   已弃置
*   ‘**home**‘ – Deprecated since version 2.2. Echo [home_url()](https://developer.wordpress.org/reference/functions/home_url/), or use bloginfo(‘url’).