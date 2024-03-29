---
title: Git学习交流
author: 千石酱
email: CN_QianShi@hotmail.com
readmore: true
hideTime: true
---
这篇文章记录了我对Git的一些理解以及Git的一些基本用法，本人才疏学浅，文章难免有错误，如果小伙伴发现了错误，请在评论区指正，我会尽快修改，欢迎大家一起学习交流！

## 预备

### 创建你的第一个仓库（以Gitee为例）
1.打开[Gitee](https://gitee.com/login)的登陆界面，并注册登录,本步骤比较简单，图略
<div class="warning">

> 注意：为了更好的使用Git，注册Gitee时最好使用邮箱注册，已有帐号也请到账号后台绑定邮箱

</div>
2.新建仓库

![新建仓库](https://pic.lengfan.me/2022/03/09/15258c0460069.png)_新建仓库_

如图所示，点击新建仓库，会跳转到如下界面：

![创建仓库](https://pic.lengfan.me/2022/03/09/45b5191815e5b.png)_创建仓库_
填入仓库名称，其他默认，点击创建，跳转到如下页面：
![仓库](https://pic.lengfan.me/2022/03/09/848648ebe468a.png)_复制_
按照图示箭头所指按钮点击复制即可，将复制的内容粘贴到记事本，备用

## 基础知识（了解）

### Git工作流程
我们的本地仓库由Git维护的三颗“树”组成，即工作目录，暂存区（Index）和HEAD
1.工作目录：相当于我们的本地文件夹，存放着我们实际操作的文件
2.暂存区（Index）：相当于一个缓存区，临时保存着我们对文件的改动
3.HEAD：保存着我们的最后一次提交的结果
Git的工作流程如下图所示

![work tree](https://pic.lengfan.me/2022/03/09/3e96513d90ffb.png)_图片来自菜鸟教程_
（感谢[菜鸟教程](https://www.runoob.com/w3cnote/git-guide.html)的图片）
在使用Git时，我们会先将文件添加到暂存区，再将这些文件提交到HEAD，最后再将文件提交到远程仓库。
看到这里有的小伙伴是不是一脸懵？是不是开始担心我学不会Git？哈哈，我当初学习Git的时候也是一脸懵。不过，小伙伴们不用担心，因为接下来，我会手把手的教你们如何提交一个文件到远程仓库，并指出其中需要注意的地方。在这个过程中，你将对上面的知识有更深的感悟。
那么。接下来，让我们开始了解Git的入门操作吧！

## 入门操作

### 设置

我们假定你已经成功安装Git，并且Git可以正常在命令行输出，我们应该使用以下指令设置你的用户名和email邮箱，以后每次提交都会使用该信息。
在这里，我们填入我们Gitee账号的用户名和邮箱即可
``` bash
$ git config --global user.name "填入用户名"  #名称
$ git config --global user.email "填入邮箱"   #邮箱
``` 
![设置用户名和邮箱](https://pic.lengfan.me/2022/03/09/5a37b4d3af3f7.png)_设置用户名和邮箱_

### 创建一个仓库
仓库是用来存放文件的一个区域，分为本地仓库和远程仓库。
我们可以使用一个已经存在的目录或者新建一个空目录来初始化仓库，命令如下：

``` bash
$ cd <目录> #在Windows系统中，你可以在文件夹中通过“shift + 鼠标右键”的形式在命令行中进入该文件夹
$ git init #初始化Git仓库
```
在这里，我在桌面创建了一个名为Git-study的文件夹，并在里面新建了一个名为one的文件夹作为工作目录。我在Git-study里打开了命令行，利用cd指令进入了one文件夹，并且进行了初始化仓库的操作
![初始化仓库](https://pic.lengfan.me/2022/03/09/8598c2bad6fad.png)_初始化仓库_
<div class="warning">

> 注意：为了更好的理解，我给每条命令前面加上了“$”符号，给每个目录名和文件名加上了"<>"符号，命令中并不包含这些符号，阅读时请注意，下同

</div>

我们也可以指定目录作为Git仓库，命令如下：

``` bash
$ git init <目录>
```

### 添加新文件
现在我们已经初始化了一个本地仓库。如果我们想要向这个仓库添加文件，我们可以使用如下命令：
``` bash
$ git add <文件名>
```
如果我们需要提交目录下所有的文件，我们可以使用如下命令：
``` bash
$ git add *
```
在这里，我在one文件夹里新建了两个txt文件，分别名为test.txt和test1.txt，并将test.txt文件提交到了暂存区
![新建两个文本文件](https://pic.lengfan.me/2022/03/09/9b4fef0ab2260.png)_新建两个文本文件_
![添加test.txt文件到暂存区](https://pic.lengfan.me/2022/03/09/18133bcefecc3.png)_添加test.txt文件到暂存区_
我们可以通过git status来查看文件的状态，如下图：
![文件提交](https://pic.lengfan.me/2022/03/09/89e750dc80065.png)_test.txt被提交了，test1.txt未被提交_
从图中我们可以看到，test.txt显示绿色，test1.txt显示红色，说明test.txt被提交了，而test1.txt未被提交
![全部提交](https://pic.lengfan.me/2022/03/09/6d5ff3742a789.png)_文件已全部提交_
使用git add *后文件就全都被提交到暂存区了

### 提交版本
现在我们已经添加了一个或者一些文件到暂存区，如果我们想将文件提交到HEAD，我们还需要输入如下指令：

``` bash
$ git commit -m "代码提交信息"
```
这段命令中的“代码提交信息”指的是我们对文件做了哪些修改，这部分需要我们自己修改。
![提交到HEAD](https://pic.lengfan.me/2022/03/09/2bbf21e9a5f76.png)_将文件提交到HEAD_
如上图，test.txt和test1.txt被成功提交到了HEAD

### 推送改动
现在，你的改动已经保存在你的本地仓库的HEAD中了。为了能够正常提交代码，我们还需要进行一些设置

``` bash
git remote add origin <server>
```
下面这个命令的意思是添加一个远程服务器到你的本地，将<server>替换为你之前复制的链接即可
![添加远程服务器](https://pic.lengfan.me/2022/03/09/9671552e1b5d2.png)_添加远程服务器_

最后，确认一切都OK，我们可以使用如下命令，愉快地提交我们的文件到Gitee上面我们创建的仓库！（撒花~~）
``` bash
$ git push origin master
``` 
![提交改动到远程仓库](https://pic.lengfan.me/2022/03/09/c70a88d025139.png)_提交改动到远程仓库_
![成功提交](https://pic.lengfan.me/2022/03/09/336f64f819bff.png)_成功提交_
