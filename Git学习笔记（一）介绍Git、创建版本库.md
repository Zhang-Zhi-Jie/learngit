一直只是简简单单的会使用git常用的功能，但是并没有系统了解Git，所以想系统记录一下Git。
本次Git系统学习主要来自[廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600)，根据他的内容系统学习一下Git知识。

---
## Git的实质
了解了Git的历史，其实可以知道Git的实质是：**区别于CVS、SVN这种集中式的版本控制系统，Git是一种分布式版本控制系统**

---

## Git的安装与配置
主要用两个系统：
- linux：直接输入 `sudo apt-get install git`，进行下载
- windows：直接下载exe文件进行安装

然后到终端输入git看是否有如下信息，有则代表安装成功
<img src = "https://img-blog.csdnimg.cn/20191214162605586.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70" width = 60%>

然后配置一下
```shell
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```
即告诉git的这台机器的用户名和Email地址

---

## Git创建版本库（仓库）
先看一张图，来自廖雪峰博客，侵删。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191214162922428.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
可见，版本库包含两个东西：**stage（暂存区）**和**master（分支）**。这两个东西之后再说。
而版本库又叫**仓库**，这个想必听得更多些。

那么，我们先创建一下版本库：
首先在合适的地方创建一个文件夹作为自己学习git的**工作区**，然后通过指令：
```shell
git init
```
得到：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191214164008224.png)
这里工作区便得到了一个`.git`目录，这个便是管理版本库的。

我们试着将一个文件添加到版本库中。
首先使用**Notepad++**来编写一个`readme.txt`文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191214164154211.png)
然后放到刚才创建的工作区`learngit`下，然后使用两个指令：
第一个：
```shell
git add readme.txt
```
这个命令是告诉Git，要将`readme.txt`添加到仓库中
第二个：
```shell
git commit -m "wrote a readme file"
```
`git commit`命令，`-m`后面输入的是本次提交的说明，可输入任意内容（最好是有意义），想到大一时做那个项目，每次提交说明就用个数字代替，最后都不知道之前修改了啥（尴尬

<img src = "https://img-blog.csdnimg.cn/20191214164459542.png" width = 60%>

而Git中的`commit`是可以一次提交多个文件的，比如这个例子：
```shell
git add file1.txt
git add file2.txt file3.txt
git commit -m "add 3 files."
```



