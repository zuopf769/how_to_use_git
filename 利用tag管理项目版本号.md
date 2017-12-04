## 利用tag管理项目版本号

> [左鹏飞](https://github.com/zuopf769) 2017.12.04


### 1. 什么是tag?什么时候应该创建一个tag?

项目的版本管理中,每当一个release版本发布时,需要做一个记录,以便以后需要的时候能查找特定的版本,这时候就用到tag这个功能.

Git中的tag指向一次commit的id，通常用来给开发分支做一个标记，如标记一个版本号。

### 2. tag和branch有什么区别？

+ branch是一个分支；tag是分支上的一个里程碑，一个点；
+ tag就是一个只读的branch；一般为每一个可发布的里程碑版本打一个tag；
+ 简单说比如branch有1.0，1.1等，其中1.0分支里可以有1.0.1，1.0.2这些tag；
+ tag就像是一个里程碑一个标志一个点; branch是一个新的征程一条线；
+ tag是静态的，branch要向前走；
+ 稳定版本备份用tag，新功能多人开发用branch（开发完成后merge到master）。


### 3. 相关操作命令

#### 3.1 打标签

```
git tag -a 0.1.3 -m “Release version 0.1.3″

```
> + git tag 是命令
  + -a 0.1.3是增加名为0.1.3的标签
  + -m 后面跟着的是标签的注释

打标签的操作发生在我们commit修改到本地仓库之后。


#### 3.2 提交

```
git add .
git commit -m “fixed some bugs”
git tag -a 0.1.3 -m “Release version 0.1.3″
```

#### 3.3 提交标签到远程服务器上

```
git push origin master
git push origin --tags

```

> + –tags参数表示提交所有tag至服务器端，普通的git push origin master操作不会推送标签到服务器端。
> + 如果指定特性的tag` git push origin [tagname] `


#### 3.4 删除标签的命令

```
git tag -d 0.1.3
```

#### 3. 5 删除远端服务器的标签

```
git push origin :refs/tags/0.1.3
```

### 参考资料

+ [Git中tag的用法](http://blog.csdn.net/jeffasd/article/details/49863335)
+ [Git 基础 - 打标签](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)
+ [GitHub实战系列~发布版本之分支操作+Tag讲解](http://www.cnblogs.com/dunitian/p/5045132.html)