---
title: wordpress - get_option()
categories:
  - 计算机
  - 网络
date: 2017-09-24 23:12:45
tags:
---
<!-- more -->
get_option( string $option, mixed $default = false )
====================================================

Description [#Description](https://developer.wordpress.org/reference/functions/get_option/#description)
-------------------------------------------------------------------------------------------------------

If the option does not exist or does not have a value, then the return value will be false. This is useful to check whether you need to install an option and is commonly used during installation of plugin options and to test whether upgrading is required. 如果不给他一个查询得值，会输出false If the option was serialized then it will be unserialized when it is returned. Any scalar values will be returned as strings. You may coerce the return type of a given option by registering an [‘option_$option’](https://developer.wordpress.org/reference/hooks/option_option/) filter callback.