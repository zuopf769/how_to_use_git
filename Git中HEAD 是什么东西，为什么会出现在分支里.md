
## 理解git中的HEAD、head和master


### 1. 概念

说简单一点，HEAD就是当前活跃分支的游标。

形象的记忆就是：你现在在哪儿，HEAD就指向哪儿，所以Git才知道你在那儿！

不过HEAD并非只能指向分支的最顶端（时间节点距今最近的那个），实际上它可以指向任何一个节点，它就是 Git内部用来追踪当前位置的东东。


### 2. HEAD和head

你可以认为 HEAD(大写)是"current branch"(当下的分支)。当你用git checkout切换分支的时候，HEAD 修订版本重新指向新的分支。有的时候HEAD会指向一个没有分支名字的修订版本，这种情况叫”detached HEAD“

head(小写)是commit对象的引用，每个head都有一个名字（分支名字或者标签名字等等），但是默认情况下，每个叫master的repository都会有一个head, 一个repository可以包含任意数量的head。在任何时候，只要这个head被选择成为”current head“，那么这个head就成了HEAD,总是大写


### 3. 图解HEAD

在master分支上，HEAD指向master，而master指向的是最近的一次提交。如下图

![1](https://github.com/zuopf769/how_to_use_git/blob/master/images/20141230143856975.png)

当我们新建分支时，比如新建分支Dev，Dev会指向当前master分支的最近一次提交。

当我们使用命令：

```
git checkout dev  

```
切换到Dev分支后，HEAD就指向当前分支Dev了。

![2](https://github.com/zuopf769/how_to_use_git/blob/master/images/20141230143916421.png)


在Dev上修改，比如修改helloworld.c，然后提交，分支Dev指向当前分支的最新提交，而master指向master分支的最新提交。

切换回到master分支：

```
git checkout master  

```

然后再master分支上查看helloworld.c，我们发现并没有被修改。

![3](https://github.com/zuopf769/how_to_use_git/blob/master/images/20141230143942948.png)

为了将在分支Dev上所做的修改也作用的master分支上，也就是说将Dev分支合并（merge）到master分支上。

```
git merge dev  

```
这时候master指向了Dev的最近一次提交。而head指向当前分支即master。

![4](https://github.com/zuopf769/how_to_use_git/blob/master/images/20141230144015116.png)

当利用分支Dev做好修改工作后，就可以把Dev删除掉。兔死狗烹，卸磨杀驴。

```
git branch -d dev  

```
![5](https://github.com/zuopf769/how_to_use_git/blob/master/images/20141230144036207.png)
