## 使用git rebase合并多次commit

### 1. 背景

一个repo通常是由一个team中的多个人共同维护，如果需要增加新feature，那么就是一个feature分支了。由于开发中各种修改，本feature分支多次commit。最后提交master后，会看到乱七八糟的所有增量修改历史。其实对别人来说，我们的改动应该就是增加或者删除，给别人看开发过程的增量反而太乱。于是我们可以将feature分支的提交合并后然后再merge到主干这样看起来就清爽多了。


记得知乎上有个帖子提问为啥vue的作者尤大大在开发vue的时候，提交历史能做到如此清爽。[Git commits历史是如何做到如此清爽的? - 知乎](https://www.zhihu.com/question/61283395)

![vue commit log](https://github.com/zuopf769/how_to_use_git/blob/master/images/v2-6351aba6f4b722630d0b3086dcab2927_hd.jpg)


### 2. rebase简介

rebase的作用简要概括为：可以对某一段线性提交历史进行编辑、删除、复制、粘贴；因此，合理使用rebase命令可以使我们的提交历史干净、简洁！

但是需要注意的是：
> 不要通过rebase对任何已经提交到公共仓库中的commit进行修改（你自己一个人玩的分支除外）


### 3. 反面例子

新建一个repo `rebase-test`；新建开发分支`dev`；在开发分支是`commit`了三次然后`merge`到`master`分支；然后`git log `或者`git log --oneline`；可以发现`dev`分支上的每次`commit `都体现到了`master`上

```
fb28c8d (HEAD -> master, origin/master, origin/dev, origin/HEAD, dev) fix: 第三次提交
47971f6 fix: 第二次提交
d2cf1f9 fix: 第一次提交
26bac61 Initial commit

```

> 如果用`git log `可以按`s`向下翻`log`
> 
> `git log --oneline` 可以一行展现


### 4. 具体操作

当我们在本地仓库中提交了多次，在我们把本地提交push到公共仓库中之前，为了让提交记录更简洁明了，我们希望把如下分支B、C、D三个提交记录合并为一个完整的提交，然后再push到公共仓库。

![rebase示意图](https://github.com/zuopf769/how_to_use_git/blob/master/images/2147642-42195cacced56729.png)

这里我们使用命令:

```javascript
git rebase -i  [startpoint]  [endpoint]

```

其中`-i`的意思是`--interactive`，即弹出交互式的界面让用户编辑完成合并操作，`[startpoint]  [endpoint]`则指定了一个编辑区间，如果不指定`[endpoint]`，则该区间的终点默认是当前分支HEAD所指向的commit(注：该区间指定的是一个前开后闭的区间)。
在查看到了log日志后，我们运行以下命令：

```
git rebase -i 36224db
```
或者

```
git rebase -i HEAD~3 

```

然后我们会看到如下界面:

![rebase示意图](https://github.com/zuopf769/how_to_use_git/blob/master/images/rebase-1.png)

上面未被注释的部分列出的是我们本次rebase操作包含的所有提交，下面注释部分是git为我们提供的命令说明。每一个commit id 前面的pick表示指令类型，git 为我们提供了以下几个命令:

> pick：保留该commit（缩写:p）
>
> reword：保留该commit，但我需要修改该commit的注释（缩写:r）
>
> edit：保留该commit, 但我要停下来修改该提交(不仅仅修改注释)（缩写:e）
>
> squash：将该commit和前一个commit合并（缩写:s）
>
> fixup：将该commit和前一个commit合并，但我不要保留该提交的注释信息（缩写:f）
>
> exec：执行shell命令（缩写:x）
>
> drop：我要丢弃该commit（缩写:d）


根据我们的需求，我们将commit内容编辑如下:

> pick d2cf1f9 fix: 第一次提交
>
> s 47971f6 fix: 第二次提交
> 
> s fb28c8d fix: 第三次提交

上面的意思就是把第二次、第三次提交都合并到第一次提交上

然后`wq`保存退出后是注释修改界面:

![rebase示意图](https://github.com/zuopf769/how_to_use_git/blob/master/images/rebase-3.png)


> 可以再浏览态 按下两个dd可以删除一行

最终的编辑效果如下：
![rebase示意图](https://github.com/zuopf769/how_to_use_git/blob/master/images/15_48_34__05_02_2018.jpg)


编辑完保存即可完成commit的合并了：

![rebase示意图](https://github.com/zuopf769/how_to_use_git/blob/master/images/15_49_16__05_02_2018.jpg)


