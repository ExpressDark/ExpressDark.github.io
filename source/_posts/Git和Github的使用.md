# Git和GitHub的使用流程

## 安装Git

计算机使用的是window系统，在Git官网上[下载]( https://git-scm.com/downloads )对应的程序。

安装完成后，在文件夹中右键鼠标出现的开始菜单中 出现“Git”->“Git Bash“，说明Git安装完成。

在命令行中输入以下，指令检查下载版本

~~~
 $git version 
~~~

可知当前电脑安装的git版本为2.24.0版本

<img src="C:\expressDark\source\picture\git\git1.png" style="zoom:100%;" />



## 创建版本库

为了方便Git管理（修改，删除，跟踪）文件，我们必须创建一个版本库（repository）。

首先选择我们要创建仓库的文件夹位置，启动git bash。

在命令行中输入以下指令

~~~
$ git init
~~~

此时可以发现在当前目录下会多一个.git文件夹，（如果没有发现，需要显示所有隐藏文件夹）。这个文件夹就是git用来跟踪管理版本的，该文件夹不能手动修改，否则会破坏版本库。

## 基本操作

### 将文件添加到本地仓

版本控制系统会跟踪文本文件的改动，因此，当我们修改文件完成后，需要将文件添加到本地仓进行管理。

在命令行中输入以下指令

~~~ 
$ git status
~~~

可以查看当前状态，如图所示，我们添加的txt发生了修改，可以将其添加到本地仓中进行更新。

![](C:\expressDark\source\picture\git\git2.png)

在命令行中输入以下指令

~~~ 
$ git add test.txt
~~~

执行指令没有任何显示说明成功将test.txt添加到本地版本库。然后需要进行添加说明，其指令为

~~~ 
$ git commit -m "修改test文件"
~~~

![](C:\expressDark\source\picture\git\git3.png)

如果出现上图所示，则说明添加说明成功，其中-m是message的缩写，“ ”内为本次修改的说明内容。为了更好的管理和修改版本库，该操作是非常有必要的，甚至为后期的回溯版本提供了足够的便利。

### 管理本地仓

之前已经使用了一种管理仓库的指令$ git status，能够让我们掌握仓库当前的状态，接下来将介绍一下其他指令；

虽然git status能够告诉我们test.txt发生了修改，但是我们并不知道哪里发生了修改，此时在命令行中输入

~~~ 
$ git diff test.txt
~~~

其效果为

![](C:\expressDark\source\picture\git\git4.png)

白色字体是未修改部分，红色字体是删除部分，绿色字体是新添加部分；

经过多次添加文件，修改文件操作后，我们可以查看所有的修改历史记录，其指令为

~~~ 
$ git log
~~~

![](C:\expressDark\source\picture\git\git5.png)

git log命令显示最近提到最远提交的所有日志，最近的一次操作是修改test文件，在往前是修改test，fix confilt，现在我们不想要这些修改信息，想进行回溯之前的版本，执行下面命令行

~~~ 
$ git reset 118ab82154f13bd38eabd8f0cd3531ea6a92ac37 
~~~

执行未出现问题的话，就回溯到了fix confilt版本，在执行git log可以看到如下效果

![](C:\expressDark\source\picture\git\git6.png)

此时使用指令$ git diff test.txt，发现当前有很多不同，原因是，工作区的文件已经进行修改，而并没有传到版本库中；为了让工作区也恢复原状，需要执行执行撤销命令

~~~ 
$ git checkout test.txt
~~~

能够获得如图效果

![](C:\expressDark\source\picture\git\git7.png)

除了在相应文件夹中删除指定的文件夹这种删除修改操作外，我们还可以用git中的rm指令用于删除文件，如果这个文件已经添加到版本库中，使用git rm指令将会永久删除该文件。



## GitHub远程仓库

[GitHub]( https://github.com/ ) 是一个提供Git仓库托管服务的远程仓库，本地Git仓库和GitHub之间的传输是通过SSH加密的，所有首先需要创建一个SSH key。

第一步：创建SSH Key。在系统盘C盘中用户文件夹中要是能找到.ssh文件夹中已经有了SSH钥匙。否则在命令行中输入以下指令

~~~ 
$ ssh-keygen -t rsa -C "youremil@163.com"
~~~

根据自己在GitHub上注册使用的邮箱，生成本地SSH key，一路按回车，使用默认值即可（不用于军事，无需设置密码）。此时能够找到.ssh文件中的两个id_rsa和id_rsa.pub两个文件，其中id_rsa是私钥，不能泄露出去，id_rsa是公钥，可以告诉他人。

第二步：登入GitHub，打开“Account settings”， “SSH keys”页面：

然后点Add SSH key，填上任意Title，在文本框中添加id_rsa.pub文件中的内容。

完成上面两步，便可以开始将本地版本库的内容传到GitHub远程仓库中了。

在此之前，可以通过以下指令检查当前设置的邮箱和用户名是否正确

~~~ 
$ git config --global --list
~~~

如果需要修改，使用如下指令

~~~ 
1. $ git config --global user.name "新的用户名"
2. $ git config --global user.email "新的邮箱"
~~~

如果更换邮箱信息，需要重新生成ssh-key，在执行一次第一步和第二步。

将本地仓库内容push到GitHub上自己建立的repository上需要执行以下指令

~~~ 
git remote add origin git@github.com:ExpressDark/test.git
~~~

这里的git@github.com:ExpressDark/test.git是SSH key。这一步的过程是把本地仓和在github上创建的远程仓库进行连接。

下一步就可以将本地仓库的内容推到远程仓库。如果是第一次

$ git push -u origin master

如果是第一次推送，因为远程仓库是空的，可以将本地仓内容推送到master分支，需要加上-u参数。之后只需要执行

~~~ 
$ git push origin master
~~~

除了上传本地仓到远程仓库操作外，还可以从远程仓库clone内容到本地进行操作，一般可能的方式有ssh或者http。克隆指令为git clone。

## 分支管理

Git把每次提交的内容串成一条时间线，这条时间线就是一条分支，这个分支在Git中成为master。一般来说，master是用来进行版本的更迭与发布，不不能轻易修改的。为此开发应该在分支上进行。

首先，我们要创建一个dev分支

$ git branch dev

然后用git branch命令查看当前分支，可以看到当前分支任然在master上，现在需要切换到dev分支上去。

切换分支的方式有两种

$ git switch dev

$ git checkout dev

当在dev分支上完成一定操作后，确定没有问题可以将dev分支上的内容合并到master分支上，首先先切换到master分支，然后执行以下指令

~~~
$ git merge <name>
~~~

删除分支的指令为

~~~
$ git branch -d <name>
~~~

软件开发中，会时常有修复bug操作，为此需要创建一个bug分支来临时修复bug，修复bug完成后，合并分支，并删除临时bug分支。

如果当手头工作没有完成时，先用git stash保存当前未完成工作，然后去修复bug，待bug完成后，使用git stash pop，回到工作现场。

## 标签管理

回溯版本时，commit号是6a4552e...，一串乱七八糟的数字不好管理，最好的办法就是是进行标签标记。

可以用git tag查看当前所有指令。标签直接执行以下命令

~~~ 
$ git tag v1.0
~~~

如果知道commit的id，可以对之前的commit进行便签处理

~~~ 
$ git tag v1.0 <id>
~~~

推送本地标签命令为

~~~ 
$ git push origin <tagname>
~~~

删除本地标签命令为

~~~
$ git tag -d <tagname> 
~~~



## 参考资料

- [廖雪峰的Git教程]( https://www.liaoxuefeng.com/wiki/896043488029600 )
- [码匠笔记的B站视频]( https://www.bilibili.com/video/av55780016 )