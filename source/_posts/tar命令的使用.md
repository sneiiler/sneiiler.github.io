---
title: tar命令的使用
date: 2018-06-02 22:35:02
tags:
---
tar

tar是在Linux中使用得非常广泛的文档打包格式。它的好处就是它只消耗非常少的CPU以及时间去打包文件，但它仅仅只是一个打包工具，并不负责压缩。
<!-- more -->

下面是如何打包一个目录：
``` bash
# tar -cvf archive_name.tar directory_to_compress
```
下面是如何解包的命令：
``` bash
# tar -xvf archive_name.tar.gz
```
上面这个解包命令将会将文档解开在当前目录下面。当然，你也可以用这个命令来更改解包的路径：
``` bash
# tar -xvf archive_name.tar -C /tmp/extract_here/
```
tar.gz

这种格式是我使用得最多的压缩格式。它在压缩时不会占用太多CPU的，而且可以得到一个非常理想的压缩率。可以使用下面的命令去压缩一个目录：
``` bash
# tar -zcvf archive_name.tar.gz directory_to_compress
```
解压缩：
``` bash
# tar -zxvf archive_name.tar.gz
```
上面这个解包命令将会将文档解压在当前目录下面。当然，你也可以用这个命令来更改解包的路径：
``` bash
# tar -zxvf archive_name.tar.gz -C /tmp/extract_here/
```
tar.bz2

这种压缩格式是我们提到的所有方式中压缩率最好的。当然，这也就意味着，它比前面的方式要占用更多的CPU与时间。下面的命令就是如何使用tar.bz2进行压缩。
``` bash
# tar -jcvf archive_name.tar.bz2 directory_to_compress
```
上面这个解包命令将会将文档解开在当前目录下面。当然，你也可以用这个命令来更改解包的路径：
``` bash
# tar -jxvf archive_name.tar.bz2 -C /tmp/extract_here/
```
下面对tar命令中一些常用重要的参数进行总结：

-c或–create 建立新的备份文件。 
-C<目的目录>或–directory=<目的目录> 切换到指定的目录。 
-f<备份文件>或–file=<备份文件> 指定备份文件。 
-j或–bzip2 以bz2的算法来压缩或者解压文件。 
-k或–keep-old-files 解开备份文件时，不覆盖已有的文件。 
-m或–modification-time 还原文件时，不变更文件的更改时间。 
-N<日期格式>或–newer=<日期时间> 只将较指定日期更新的文件保存到备份文件里。 
-r或–append 新增文件到已存在的备份文件的结尾部分。 
-t或–list 列出备份文件的内容。 
-u或–update 仅置换较备份文件内的文件更新的文件。 
-v或–verbose 显示指令执行过程。 
-w或–interactive 遭遇问题时先询问用户。 
-W或–verify 写入备份文件后，确认文件正确无误。 
-x或–extract或–get 从备份文件中还原文件。 
-z或–gzip或–ungzip 通过gzip指令处理备份文件。 
-Z或–compress或–uncompress 通过compress指令处理备份文件