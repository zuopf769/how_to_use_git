## 使用git rebase合并多次commit

### 1. 背景

一个repo通常是由一个team中的多个人共同维护，如果需要增加新feature，那么就是一个feature分支了。由于开发中各种修改，本feature分支多次commit。最后提交master后，会看到乱七八糟的所有增量修改历史。其实对别人来说，我们的改动应该就是增加或者删除，给别人看开发过程的增量反而太乱。于是我们可以将feature分支的提交合并后然后再merge到主干这样看起来就清爽多了。


记得知乎上有个帖子提问为啥vue的作者尤大大在开发vue的时候，提交历史能做到如此清爽。[Git commits历史是如何做到如此清爽的? - 知乎](https://www.zhihu.com/question/61283395)


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


### 4. 如何使用rebase合并多个commit为一个完整commit

当我们在本地仓库中提交了多次，在我们把本地提交push到公共仓库中之前，为了让提交记录更简洁明了，我们希望把如下分支B、C、D三个提交记录合并为一个完整的提交，然后再push到公共仓库。



这里我们使用命令:

```javascript
git rebase -i  [startpoint]  [endpoint]

```

其中`-i`的意思是`--interactive`，即弹出交互式的界面让用户编辑完成合并操作，`[startpoint]  [endpoint]`则指定了一个编辑区间，如果不指定`[endpoint]`，则该区间的终点默认是当前分支HEAD所指向的commit(注：该区间指定的是一个前开后闭的区间)。
在查看到了log日志后，我们运行以下命令：
















