---
title: Git多账号、密钥管理
date: 2018-06-01 11:26:11
categories:
  - 计算机
  - 网络
tags:
---
有的时候有多个账号和Git提交需求，这就需要同时配置多个密钥对，通过SSH的方式进行git提交。

<!-- more -->

首先生成SSH-KEY
==============

打开命令行、终端，用命令进入到你要保存SSH-KEY文件的文件夹，我们先用命令测试下终端是否支持SSH：

``` bash
ssh -V
```

测试时如果提示不识别SSH命令，需要安装SSH。
Ubuntu安装SSH：
``` bash
sudo apt-get install openssh-client openssh-server
```
CentOS安装SSH：
``` bash
yum install openssh-client openssh-server
```

Windows可以在当前文件夹右键，选择Git Bash Here，会自动在当前文件夹打开一个MINGW的命令行窗体，它是自带SSH的。

接下来进入ssh保存公钥和密钥的文件夹，使用SSH命令在当前文件夹生成一对SSH-KEY：

``` bash
ssh-keygen -t rsa -C "邮箱地址"
```

接下来会出来提示信息，完整的大概是这样：

``` bash
$ ssh-keygen -t rsa -C "smallajax@foxmail.com"
Generating public/private rsa key pair.
Enter file in which to save the key (~/.ssh/id_rsa):
```

这里需要输入SSH-KEY的文件名字，这里名字理论上可以随便取，根据爱好输入KEY文件的名字吧，例如为Github配置就输入：id_rsa_github，为OSChina配置就输入：id_rsa_oschina。

接着会要求输入私钥的密码，并且需要确认密码，为了安全在密码输入的时候不会反显，什么都看不到，这个密码你自己设置，但是你一定要记住：
``` bash
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```
到这里生成SSH-KEY的事就完成了，你在当前文件夹会看到两个文件：
```
id_rsa_github  id_rsa_github.pub
```

SSH-KEY生成了，接着给服务器和客户端配置SSH-KEY
- 第一步把id_rsa_github.pub中的公钥内容添加到Git的SSH中，如果你使用Github或者Gitlib，在个人设置中会找到。
- 第二步为SSH配置私钥位置，这里和上面配置单个Git帐号不一样，不过单个帐号也可以按照多个帐号的配置方法来配置。

下面我们需要在.ssh文件夹新建一个名为config的文件，用它来配置多个SSH-KEY的管理。

Linux进入.ssh文件夹：cd ~/.ssh，新建config文件：touch config；或者：touch ~/.ssh/config。这里要注意，没有.ssh文件夹的要新建一个.ssh名的文件夹。

Window进入C:/Users/你的用户名/.ssh文件夹，右键新建一个文本文件，改名为config即可。这里要注意，没有.ssh文件夹的要新建一个.ssh名的文件夹。

下面来填写config文件的内容，我以Github、Gitlib、OSChina，局域网为例：

```
Host github.com
    HostName github.com
    User smallajax@foxmail.com
    PreferredAuthentications publickey
    IdentityFile /home/Workspace/ssh/id_rsa_github
Host gitlib.com
    HostName gitlib.com
    User smallajax@foxmail.com
    PreferredAuthentications publickey
    IdentityFile id_rsa_gitlib
Host oschina.com
    HostName oschina.com
    User smallajax@foxmail.com
    PreferredAuthentications publickey
    IdentityFile /D/Workspace/ssh/id_rsa_oschina
Host 192.168.1.222
    HostName 192.168.1.222
    User smallajax@foxmail.com
    PreferredAuthentications publickey
    IdentityFile /D/Workspace/ssh/id_rsa_oschina
```

解释一下，HostName是服务器的地址，User是用户名，PreferredAuthentications照抄即可，这里主要说的是IdentityFile，上面我们看到了三种情况，所以它的书写原则是：

填私钥文件的本地路径。

不论是Linux还是Windows都可以写相对路径，比如把id_rsa_xxx私钥文件放在.ssh文件夹下。

文件放在不同跟路径下时，需要写绝对路径 

Linux中没有放在.ssh文件夹内或者子文件夹。

Windows中没有放在C盘下时。注意据对路径变化，比如C盘下是/C/xo/abc、比如D盘下/D/ssh/id_rsa这样，还看不懂请参考上方例子。
拷贝完成后，把所有的id_rsa私钥文件添加到SSH-Agent，命令如下：
``` bash
ssh-add id_rsa文件的路径
```

例如添加.ssh文件夹下的，Linux这样做：ssh-add ~/.ssh/id_rsa，如果你在.ssh文件夹下：ssh-add id_rsa即可，Windows同理。

此时添加时如果遇到错误，请参考本文最后一节：添加SSH到SSH-Agent时报错。

最后，还剩下项目的用户和邮箱没有配置，和配个单个Git帐号的方式不同，这里我们需要为每个项目分别配置，所以要命令行进入仓库文件夹再设置。第一种情况是先从Git上pull仓库下来，第二种情况是本地初始化Git仓库，总之进入改仓库文件夹后：
``` bash
git config --local user.name "你的名字"
git config --local user.email "你的邮箱"
```

不过麻烦的一点是如果是多个项目就需要挨个配置，不过我们一般是pull一个项目就配置一下，也仅仅需要配置一次即可。

注意配置单个Git帐号时，是不进入项目文件夹就可以，不过不是使用--local，而是使用--global就可以全局配置。

配置项目用户和邮箱完成后，我们可以进入项目文件夹下的.git文件夹查看config文件内容，大概内容如下：
```
...
[user]
    name = YanZhenjie
    email = smallajax@foxmail.com
```
此时配置全部结束，请查看下方测试SSH-KEY配置是否成功进行测试。如果配置成功，你就可以clone和commit了。

测试SSH-KEY配置是否成功
配置全部结束，我们来测试一下配置是否成功：

如果你是Github
``` bash
ssh -T git@github.com
```
如果是你Gitlib
``` bash
ssh -T git@gitlib.com
```
如果你是局域网192.168.1.222
``` bash
ssh -T git@192.168.1.222
```
其它自行举一反三吧。
此时需要输入刚才生成SSH-KEY时输入的私钥密码，输入后自行观察信息判断是否连接成功。

比如Github的信息是：
``` bash
Hi kaifeng! You've successfully authenticated, but GitHub does not provide shell access.
```
比如Gitlib的信息是：
``` bash
Welcome to GitLab, YanZhenjie!
```
如果不能执行测试命令或者提示什么错误了，请执行ssh-agent bash完后再执行测试命令，如果还不行就是配置有问题了。

添加SSH到SSH-Agent时报错
如果执行ssh-add ...命令提示如下错误：
``` bash
Could not open a connection to your authentication agent.
```
那么请执行eval \$(ssh-agent)命令后再重试，如果还不行，请再执行ssh-agent bash命令后再执行eval \$(ssh-agent)后执行添加命令。另外上述测试配置的命令不能执行时也可以在ssh-agent bash执行完后再测试。
