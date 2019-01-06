# Git 安装与使用

## 一、基本操作

### 1. 下载安装

下载对应的[Git](https://git-scm.com/)版本安装

### 2. 配置Git

打开Git bash，配置用户名及邮箱

```bash
$ git config --global user.name "My Name"
$ git config --global user.email  "myEmail@example.com"
```

### 3. 创建一个新仓库 – git init

git会把所有文件以及历史记录直接记录成一个文件夹保存在你的项目中。

创建一个新的仓库，首先要去到项目路径下，执行`git init`。这时Git会创建一个隐藏的文件夹*.git*，所有的历史和配置信息都储存在其中。

```bash
$ cd /c/Users/zgldo/doinggit
$ git init 
```

命令行出现

```bash
Initialized empty Git repository in /c/Users/zgldo/doinggit/.git/
```

这说明我们的仓库已经建立好了，但现在是空的，试着新建一个文件(例如：README.md)到这个文件夹里。

### 4. 检查状态 – git status

`Git status`是另一个非常重要的命令，它反馈给我们仓库当前状态的信息：是否为最新代码，有什么更新等等。在我们新建的仓库中执行`git status`会得到以下内容:

![Git_status命令结果](D:\ZGLDoingGitRepository\DoingGit\应用使用总结\image\Git_status命令结果.png)

反馈信息告诉我们，(例如：README.md)尚未跟踪，这是说这个文件是新的，git不知道是应该跟踪它的变动还是直接忽略。为了跟踪我们的新文件，我们需要暂存它。

### 5. 暂存 – git add

Git有个概念叫*“暂存区“*，你可以把它看成一块空白的画布，包裹着所有你可能会提交的变动。它一开始是空的，可以通过 git add命令添加内容，最后使用 *git commit* 提交（创建一个快照）。

这个例子中只有一个文件，让我们先add它：
```bash
$ git add README.md
```
如果需要提交目录下的所有内容，可以这样做：
```bash
$ git add -A # 提交所有变化
$ git add -u # 提交被修改(modified)和被删除(deleted)文件，不包括新文件(new)
$ git add .  # 提交新文件(new)和被修改(modified)文件，不包括被删除(deleted)文件
```
再次使用git status查看状态试试：

![Git_add_之后的status](D:\ZGLDoingGitRepository\DoingGit\应用使用总结\image\Git_add_之后的status.png)

我们的文件已经准备好可以提交了。状态信息还告诉我们暂存区文件发生了什么变动，这里我们新增了一个文件，同样可以做修改和删除。取决于我们在上一次*git add*之后发生了什么。

### 6.提交 – git commit

一次提交代表着我们的仓库到了一个新的状态，就像是一个快照，允许我们像使用时光机一样回到之前的某个时间点。

创建提交，需要我们至少在到暂存区有一次修改（刚才我们做了*git add*），然后输入命令：
```bash
$ git commit -m "修改注释."
```
这就创建了一次从暂存区的提交（加入README.md），*-m “修改注释.”*是用户对这次提交的描述，建议写成有意义的描述性信息。

### 7. 查看修改内容

```bash
$ git diff 文件名+类型
```

![查看修改内容](D:\ZGLDoingGitRepository\DoingGit\应用使用总结\image\Git_diff.png)

### 8. 查看文件内容

```bash
$ cat 文件名
```

![查看文件内容](D:\ZGLDoingGitRepository\DoingGit\应用使用总结\image\cat_查看文件内容.png)

## 二、远程仓库

到目前为止，我们的操作都是在本地的——只存在于*.git*文件中。为了能够协同开发，我们需要把代码部署到远程仓库服务器上。

### 1. 链接远程仓库 – git remote add

为了能够上传到远程仓库，我们需要先建立起链接。在这篇教程中，我们远程仓库的地址为：<https://github.com/zgldoing/DoingGit.git>。但你应该自己在Github、或BitBucket上搭建仓库，自己一步一步尝试。

把本地仓库链接到Github上，在命令行执行以下内容：
```bash
# This is only an example. Replace the URI with your own repository address. 
$ git remote add origin https://github.com/zgldoing/DoingGit.git
```
一个项目可以同时拥有好几个远程仓库，为了区分通常会起不同的名字。通常主要的远程仓库被称为*origin*。

### 2.上传到服务器 – git push

把本地的提交传送到服务器的动作叫做*push。*每次我们要提交修改到服务器上时，都会使用到`git push`。

`git push`命令有两个参数，远程仓库的名字，以及分支的名字：
```bash
# $ git push origin master 
$ git push
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 297 bytes | 297.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/zgldoing/DoingGit.git
   7e26bc1..3ec5f5d  master -> master
```
取决于你使用的服务器，push过程中你可能需要验证身份（输入用户名、密码，请先在网站上进行注册）。如果没有出差错，现在用浏览器看你的远程仓库上已经有*README.md*了。

 

### 3.克隆仓库 – git clone

其他人可以看到你放在Github上的开源项目，他们可以用*git clone*命令下载到本地。
```bash
$ git clone https://github.com/zgldoing/DoingGit.git
```
本地也会创建一个新的仓库，并自动将github上的版本设为远程仓库。

### 4.从服务器上获得修改 – git pull

如果你更新了远程仓库上的内容，其他人可以通过*git pull*命令拉取你的变动：
```bash
$ git pull origin master 
From https://github.com/zgldoing/DoingGit.git
* branch            master     -> FETCH_HEAD 
Already up-to-date.
```
因为在我们`git clone`之后还没有提交过修改，所有没有任何变动。



