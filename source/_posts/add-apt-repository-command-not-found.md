---
title: 'add-apt-repository: command not found'
url: 51.html
id: 51
categories:
  - 计算机
  - shell
date: 2017-10-03 09:31:54
tags:
---

在Ubuntu下，时不时会有这个错误的。

<!-- more -->

{% codeblock %}
add-apt-repository: command not found
{% endcodeblock %}
这个是缺少程序，安装一下就可以了。只是不知道安装的名字。 按以下命令走一趟就可以的了。

``` bash
$ sudo apt-get install software-properties-common python-software-properties
```

完成这个，就可以使用add-apt-repository命令了。