---
title: LaTeX - 修改章节号
categories:
  - LaTeX
date: 2017-09-25 11:13:08
tags:
---

章节样式之一的是数字计数器的样式，如下是一个简单的示例。
<!-- more -->
更多数字的样式如下：

 arabic 阿拉伯数字
 roman 小写的罗马数字
 Roman 大写的罗马数字
 alph 小写字母
 Alph 大写字母
 
 演示示例： 
 
 
``` latex
documentclass{article} 
pagestyle{empty} 
setcounter{page}{6} 
setlength textwidth{207.0pt} 
renewcommand
  thesection{
    Alph{section}
  } 
begin{document} 
  section{Different-looking section} 
  subsection{Different-looking subsection} 
    Due to the default definitions not only the numbers on sections change, but lower-level sectioning commands also show this representation of the section number. 
end{document}
```
