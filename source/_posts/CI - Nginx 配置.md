---
title: CI - Nginx 配置
categories:
  - 计算机
  - 网络
date: 2017-09-27 23:01:54
tags:
---

配置Nginx时候需要配置index.php的转发：
配置如下：

{% codeblock lang:shell %}
{% raw %}
 server {
   listen 80;
   server_name example.com;//自己的域名
   root /alidata/www/example; //网站目录
   index index.php index.htm index.html;
   location / { 
     try_files $uri $uri/ /index.php;
   } 
   location /index.php{ 
     fastcgi_pass 127.0.0.1:9000;
     fastcgi_param SCRIPT_FILENAME /alidata/www/example/index.php;
     fastcgi_param PATH_INFO $fastcgi_path_info;
     fastcgi_split_path_info ^(.+\\.php)(.*)$;
     fastcgi_param PATH_TRANSLATED $document_root$fastcgi_path_info;
     include fastcgi.conf;
   } 
  }
{% endraw %}
{% endcodeblock %}
