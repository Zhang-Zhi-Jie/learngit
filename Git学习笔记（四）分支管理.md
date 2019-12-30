# 分支管理
## 1 创建与合并分支
我们知道Git把每次的提交都串成一条线性的时间线，这个时间线就是一个分支，我们当前的分支是 **主分支**即  `master` 分支，而 `HEAD` 指向的便是 `master`，即指向的是当前分支。

一开始，master分支是一条线，Git用master指向最新的提交，再用HEAD指向master，就能确定当前分支，以及当前分支的提交位置。而每次提交，master分支都会向前移动一步，这样，随着你不断提交，master分支的线也越来越长。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218205257218.png)
当我们创建新的分支，例如 `dev` 时，Git新建了一个指针叫dev，指向 `master` 相同的提交，再把 `HEAD` 指向dev，就表示当前分支在dev上：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218205416953.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
我们可以通过 `git checkout`命令加上 `-b` 参数表示创建并切换，相当于下面两条命令：
```shell
git branch dev
git checkout dev
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218205841265.png)
然后通过 `git banch` 查看所有分支，`*` 表示当前的分支：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218210035296.png)
我们还可以通过指令 `git switch -c dev` 指令来切换到新的 `dev` 分支，而若直接切换已有的 `master` 分支，只需要 `git switch master`。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218211018398.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)

之后，一旦对工作区进行修改并提交，则就是针对 `dev` 这个分区了，比如新提交一次后，是 `dev` 往前移动一步，`master` 没有移动。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218205535216.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
我们现在修改一下 `readme.txt` 并在 `dev` 分支上进行提交：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218210232253.png)
我们切换回 `master` 分支，查看一下 `readme.txt` 的内容。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218210356647.png)
可以发现没有新增的内容，这是因为刚才的提交只是在 `dev` 上。

假如当我们在 `dev` 上的工作完成了，就可以把 `dev` 合并到 `master` 上。最简单的方法是直接把 `master` 指向 `dev` 的当前提交，就完成了合并：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019121820563987.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
所以Git的分支合并就需要改改指针即可。

我们使用 `git merge` 命令将指定分支与当前分支进行合并，再查看文档内容，发现这与 `dev` 最新提交的内容是一致的。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218210624315.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
合并完分支后，甚至可以删除 `dev` 分支。删除dev分支就是把dev指针给删掉，删掉后，我们就剩下了一条`master` 分支：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218205707622.png)
我们通过 `git branch -d` 来删除指定分支，再查看所有分支，发现只有 `master`。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218210656309.png)
总结：

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>` 或者 `git switch <name>`

创建+切换分支：`git checkout -b <name>` 或者 `git switch -c <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`

## 2 解决冲突
我们先分出一个分支 `feature1` 进行新分支开发。

先将 `readme.txt` 修改一下，并在 `feature1` 分支上提交：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218211325285.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218211419331.png)
然后切换回 `master` 分支，这里提示我们当前 `master` 分支比远程的 `master` 分支要超前1个提交。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218211509106.png)
然后我们在master分支上修改`readme.txt`为（上面是AND，这里是 &）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/201912182116153.png)
我们提交一下，这样 `master` 分支和 `feature1` 分支各自都分别有了新的提交，这样就出现了这两个分支 **“分道扬镳”**的情况。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218211657527.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
在这种情况下，Git只能试图把各自的修改合并起来，但会出现冲突：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218211913992.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
图上已经明确提示，合并后文档出现了冲突。

接下来，我们再在 `master` 分支上修改一下 `readme.txt` 文件，并提交：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218213135686.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218212703309.png)
这样 `master` 分支和 `feature1` 分支变成了如下所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019121821271517.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
我们可以通过 `git log` 查看分支的合并情况：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218212843381.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
最后删除`feature1`分支。

## 3 分支管理策略 
通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
我们在合并分支时可以加上 `--no--ff`的参数，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218214154242.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
在实际开发中，应该按照几个基本原则进行分支管理：
首先，`master` 分支应该是非常稳定的，也就是仅用来**发布新版本**，平时不能在上面干活，而干活都在 新开的`dev`分支上，到某个时候，再把dev分支合并到master上，在master分支发布新版本；
团队每个人都在dev分支上干活，而每个人都有自己的分支，时不时地往dev分支上合并就可以了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191218214431874.png)
## 4 Bug分支
首先将当前git状态修改为这样：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191219183612361.png)
但这时接到一个需要修复一个bug的任务，这时我应该创建一个分支 `issue-101` 来修复。但是当前的 `dev` 上进行工作只做完了一半，还不能提交，可又急需修复bug，这时该怎么办？
Git提供了一个 `stash` 来存储当前工作现场，等以后恢复现场后继续工作。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191219191711663.png)
现在查看状态就是clean的。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191219192328738.png)
## 5 Feature 分支
在软件开发中，时不时需要添加新的功能。
当添加一个新功能时，肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新能，最好新建一个 `feature` 分支，在上面开发，完成后，合并，最后，删除该 `feature` 分支。
一旦在 `feature` 分支上开发完，这时若突然接到领导通知说新功能不再维护，所以这个需要将这个分支立即删除：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191223213418235.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
我们发现销毁失败。Git友情提醒，`feature-vulcan` 分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用大写的 `-D` 参数。那么我们强行删除：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191223213500563.png)

## 6 多人协作
可以通过 `git remote` 来查看远程库的信息：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191223214113310.png)
### 推送分支
推送分支即把该分支上的所有**本地**提交推送到**远程库**。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：
	![在这里插入图片描述](https://img-blog.csdnimg.cn/20191223214231641.png)
如果要推送其他分支，比如 `dev`，就改成
> git push origin dev

但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？

- `master` 分支是**主分支**，因此要**时刻与远程同步**；

- `dev` 分支是**开发分支**，团队所有成员都需要在上面工作，所以也**需要与远程同步**；

- `bug` 分支只用于**在本地修复bug**，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

- `feature` 分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

### 抓取分支
多人协作时，大家都会往 `master` 和 `dev` 分支上推送各自的修改。若推送失败，主要是因为同伴已经推送上去了，而他的最新提交和你试图推送的提交有冲突。Git这时会提示我们，先用 `git pull` 把最新的提交从`origin/dev` 抓下来，然后，在本地合并，解决冲突，再推送。
若 `git pull` 也失败了，这是因为没有指定本地 `dev` 分支与远程 `origin/dev` 分支的**链接**`在这里插入代码片`，根据提示，设置dev和origin/dev的链接：
>git branch --set-upstream-to=origin/dev dev

然后再合并，最后push。


## 7 Rebase
rebase操作可以把本地未push的分叉提交历史整理成直线；

rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

rebase的理解可以看这篇git官方文档中的解释：
[rebase from git community book](http://gitbook.liuhui998.com/4_2.html)
