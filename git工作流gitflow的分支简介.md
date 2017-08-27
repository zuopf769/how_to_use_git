# 简单介绍git工作流gitflow的分支

> 左鹏飞 2017.8.27

## 一、gitflow
+ 1、gitflow定义了一个围绕项目发布的严格的分支模型
+ 2、gitflow仍然用中央仓库作为所有开发者的交互中心。

## 二、gitflow包括哪些分支

+ master: maseter主分支，存储正式发布的历史。发布的时候会打个tag，也就是版本号
+ hotfix: 上线分支，bug情急修复分支
+ release：发布分支，发布上线的时候用
+ develop：开发分支，作为功能的收集分支
+ feature：功能分支，每次开发新功能的时候都会有对应的feature分支，同时会有几个不同的feature分支

## 三、各个分支之间的交互
+ develop分支是从master主干checkout出来的
+ feature分支是从develop分支checkout出来的，feature分支功能开发完成后会merge回develop分支
+ 同时可能会有多个feature分支，处理不同的功能
+ develop分支开发到一个里程碑的时候，就需要合入到release分支，用于QA测试回归，如果没有问题，就merge回master主干，然后在主干上release一个版本
+ 当线上出现紧急bug时，可以从master主干checkout一个hotfix分支，修复完bug后，merge会主干，紧急release一个新的版本；然后hotfix分支需要合并到develop分支，因为develop分支需要和master分支保持同步
+ hotfix分支、release分支、feature分支完成使命后就可以删掉了，而master，和develop分支始终都存在

## 四、历史分支和功能分支的区别

### 历史分支
> 相对使用仅有的一个master分支，Gitflow工作流使用2个分支来记录项目的历史。master分支存储了正式发布的历史，而develop分支作为功能的集成分支。这样也方便master分支上的所有提交分配一个版本号。

### 功能分支
> 每个新功能位于一个自己的分支，这样可以push到中央仓库以备份和协作。但功能分支不是从master分支上拉出新分支，而是使用develop分支作为父分支。当新功能完成时，合并回develop分支。新功能提交应该从不直接与master分支交互。


## 五、gitflow示意图



