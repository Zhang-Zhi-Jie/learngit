# 远程仓库
## 添加远程库
我们首先在github上添加我们电脑的SSH Key，
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191217212105298.png)
这样才能在本地将仓库push到github上。
然后我们在github上创建一个仓库，名字设为`learngit`，接着在本地`learngit`仓库下运行：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019121721230032.png)
即将本地仓库与github上的仓库进行关联，
最后，在push上去：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191217212337135.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
把本地库的内容推送到远程，用 `git push` 命令，实际上是把当前分支 `master` 推送到远程。

由于远程库是空的，我们第一次推送 `master` 分支时，加上了 `-u` 参数，Git不但会把本地的 `master` 分支内容推送的远程新的 `master` 分支，还会把本地的 `master` 分支和远程的 `master` 分支关联起来，在以后的推送或者拉取时就可以简化命令。
