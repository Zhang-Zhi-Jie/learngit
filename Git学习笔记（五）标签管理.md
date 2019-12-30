## 1 创建标签
我们可以在git上打标签。首先切换到需要打标签的分支上，然后使用命令 `git tag <name>` 即可打标签，并可用 `git tag` 查看所有标签：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224205215410.png)
默认标签是打在最新提交的commit上的，若想在过去的提交上打标签则需要找到历史提交的commit id，然后打上标签即可。
比如我想在`add test.txt`这个commit上打个标签，就可以这样：
>tag v0.9 8b10e9a
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224205436527.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2thcnJ5X3p6ag==,size_16,color_FFFFFF,t_70)

通过 `git tag` 就可以查看新增的标签了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224205547903.png)
注意，标签不是按时间顺序列出，而是按字母排序的。

还可以创建带有说明的标签，用 `-a` 指定标签名，`-m` 指定说明文字，然后通过 `git show <tagname>` 来看到说明的文字：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224205750599.png)

## 2 操作标签
- 命令`git push origin `可以推送一个本地标签；
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224210330295.png)
- 命令`git push origin --tags`可以推送全部未推送过的本地标签；
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224210353649.png)
- 命令`git tag -d `可以删除一个本地标签；
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224210259910.png)
- 命令`git push origin :refs/tags/`可以删除一个远程标签（先删除本地标签，然后再删除远程标签）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191224210518869.png) 

