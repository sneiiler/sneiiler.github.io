---
title: 修改Anaconda中的Jupyter Notebook默认工作路径-update
date: 2018-08-15 12:59:51
tags:
---
一般默认工作路径是Documents目录，但是项目不希望放在这里，可以采用这种方法修改默认工作目录：
<!-- more -->
1. 激活所需要的工作环境：`activate mne`
2. 利用命令生成`jupyter notebook`的配置文件：
``` bash
jupyter notebook --generate-config
```
3. 可以看到生成了`jupyter_notebook_config.py`文件（利用everything搜索）
4. 打开文件，找到并修改：

``` python
## The directory to use for notebooks and kernels. 
c.NotebookApp.notebook_dir = 'xxx' #这里修改为工作目录，Windows环境下用双斜杠
```

5. 重启`jupyter notebook`即可
