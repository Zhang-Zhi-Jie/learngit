# 修改版本与回退

## Git修改
我们修改一下`readme.txt`文件：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191214165004719.png)
然后我们使用`git status`查看一下仓库的状态。

<img src = "https://img-blog.csdnimg.cn/20191214164955784.png" width = 60%>

因为这个readme.txt受Git所管理，所以一旦修改之后，查看git仓库的状态就能显示出来修改记录（上图标红处），然后通过
`git diff`来查看修改前后的差异：

<img src = "https://img-blog.csdnimg.cn/2019121416514528.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70" width = 60%>

从上面可以看到修改是多加了个"distributed"。

接着，我们再`add`一下修改后的`readme.txt`，然后在`commit`之前查看一下仓库的状态
<img src = "https://img-blog.csdnimg.cn/20191214165725267.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70" width = 60%>

然后commit，并查看status，发现当前没有需要提交的修改，且工作目录是clean的

## Git版本回退
我们可以通过`git log`来查看git 日志，加上`--pretty=oneline`可以更加简洁看到git历史日志。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191214170808386.png)
从上图可以看到，每一条记录前都有一串数字+字母的号，这个就是`commit id`。

然后我们通过`git reset -- hard Head^`回退到前一个版本，`Head^`表示回退**一**个版本，那么`Head^^`表示回退**两**个版本，若想回退多个版本（举例10），就用`Head~10`。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191214171039351.png)
如果我们还想回到最新的版本，因为 append GPL的commit id为如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019121417212928.png)
所以可指定回到未来的某个版本，版本号没必要写全，前几位（4位）就可以了，Git会自动去找。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019121417131432.png)
当用 `git reset --hard HEAD^` 回退到add distributed版本时，再想恢复到append GPL，就必须找到append GPL的commit id。Git提供了一个命令`git reflog`用来记录你的每一次命令：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191214171534352.png)

## 工作区和暂存区
之前我们已经提到了这两个概念，接下来具体来了解一下这些概念。
这个就是我们的工作区：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191214182917697.png)
而这个文件夹里有一个`.git`就是Git的版本库。
Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。

我们试图去.git里找一下HEAD文件。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191214184539651.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
打开可以看到：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191214184608504.png)
然后我们打开`refs/heads/master`：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191214184649688.png)
可以发现HEAD就是指向当前的Commit id。

而我们之前的两个操作`add`和`commit`的指示图如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191214184435364.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
- `add`：将文件修改添加到暂存区stage中。
- `commit`：把暂存区的所有内容提交到当前分支。

当我们创建Git版本库时，Git会自动创建了唯一的一个master分支，所以，现在，git commit就是往master分支上提交更改。而需要提交的文件修改都放到暂存区中，再一次性commit这些修改。

我们修改一下`readme.txt`，并增加一个`LICENSE`文件，然后查看一下status。

<img src = "https://img-blog.csdnimg.cn/20191214190105367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70" width = 60%>

可以发现LICENSE没有被添加，所以状态是`Untracked`。然后我们add一下这两个文件，再查看一下status。

<img src = "https://img-blog.csdnimg.cn/20191214190218611.png" width = 60%>

这样暂存区的状态变成了这样：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191214190709219.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)


所以，`git add`实际上是把要提交的所有修改放到暂存区(Stage)，然后，执行`git commit`就可以一次性把暂存区的所有修改提交到分支。

<img src = "https://img-blog.csdnimg.cn/20191214190620199.png" width = 60%>

这样整个状态如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191214190655173.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
## 管理修改
Git管理的不是文件，而是**修改**。
修改`readme.txt`为如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191216191307496.png)
然后`git add readme.txt`，并`git status`：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191216191344588.png)
再修改 `readme.txt` 如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191216191404196.png)
然后 `git commit` 一下并查看状态：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019121619143834.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
从红色提示的字可以发现第二次的修改并没有提交，那么操作过程其实是这样的：
第一次修改 --> `git add`--> 第二次修改 --> `git commit`，所以只add了一次，所以第二次修改并没有放到暂存区，那么commit自然也不会把第二次的修改提交上去。

我们用 `git diff HEAD --readme.txt`命令来查看工作区和版本库里面最新版本的区别。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191216191735895.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
若我们 `add` 一下，并再一次 `commit` ，便可以发现 `diff `没有结果显示了：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191216191832343.png)

---

## 撤销修改
当我们不注意修改成一个错误的内容，当在提交这个修改之前，我们可以很容易地纠正它。你可以删掉最后一行，手动把文件恢复到上一个版本的状态。如果用 	`git status` 查看一下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191216192527429.png)
即我们可以用 `git restore file` 来丢弃工作区中的修改，但有两种情况：
1. `readme.txt` 从修改之后就没有被放到暂存区中，撤销修改就回到和版本库一模一样的状态。
2. `readme.txt` 已经 `add` 到暂存区中，又作了修改，撤销修改就回到添加到暂存区后的状态。

我们先修改一下 `readme.txt` ：
![在这里插入图片描述](https://img-blog.csdnimg.cn/201912161930085.png)
然后我们不 `add` 其到暂存区，尝试一下 `restore` 一下
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191216192914620.png)
然后就发现已经回到修改前的状态了。
但如果我们 `add` 这个修改，但庆幸没有commit，所以我们再 `commit` 之前查看一下状态：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191216193311637.png)
可以发现使用 `git restore --staged file` 可以把暂存区的修改撤销掉（unstage），重新放回工作区。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191216193550296.png)
然后再使用 `git restore file` 来撤销到修改前的工作区状态
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191216193659873.png)
可以发现修改已经没了。

总结一下：
- 没有add修改时，使用 `git restore file` 撤销修改；
- 已经add修改，还未commit修改，使用 `git restore --staged file` 撤销修改到原来暂存区状态，然后再 `git restore file` 撤销修改到原来工作区的状态。

---

## 删除文件
我们新建一个 `test.txt` 文件，然后 `add, commit`，接着我们使用 `rm test.txt` 删除这个文件（即相当于直接在文件），再来查看一下状态：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191216195531267.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)
可以发现，工作区和版本库不一致：因为已经add并commit了，所以版本库中有test.txt，而工作区没有了。
接下来有两种选择：
- 确认要删除，则把版本库中的也删除，使用 `git rm` 删除并 `git commit`：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019121620043272.png)
- 删错了，因为版本库里还有呢，所以可以使用 `git restore file` 把误删的文件恢复到最新版本（即撤销删除这个修改）。
