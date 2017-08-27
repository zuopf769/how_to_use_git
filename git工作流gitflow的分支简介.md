# 简单介绍git工作流gitflow的分支

> 左鹏飞 2017.8.27

## 一、gitflow
+ 1、gitflow定义了一个围绕项目发布的严格的分支模型
+ 2、gitflow仍然用中央仓库作为所有开发者的交互中心。

gitflow示意图

![gitflow示意图](https://github.com/zuopf769/how_to_use_git/blob/master/images/58e8eb560001ecfd12800720.jpg)

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


![历史分支和功能分支的区别](https://github.com/zuopf769/how_to_use_git/blob/master/images/58a025c200016a8712800720.jpg)

### 历史分支
> 相对使用仅有的一个master分支，Gitflow工作流使用2个分支来记录项目的历史。master分支存储了正式发布的历史，而develop分支作为功能的集成分支。这样也方便master分支上的所有提交分配一个版本号。

### 功能分支

#### 基本概念

> 每个新功能位于一个自己的分支，这样可以push到中央仓库以备份和协作。但功能分支不是从master分支上拉出新分支，而是使用develop分支作为父分支。当新功能完成时，合并回develop分支。新功能提交应该从不直接与master分支交互。
feature分支是从develop打出来的。

#### 使用原则

+ 新功能提交应该从不直接与master分支交互。
+ 分支名称feature/[feature name]。

### 工作流程

+ 使用develop分支作为父分支，
+ 每个新功能位于一个自己的分支
+ 新功能完成后，合并回develop分支。

#### 使用规范
+ 可以从develop分支发起feature分支
+ 代码必须合并回develop分支
+ feature分支的命名可以使用除master，develop，release-*，hotfix-*之外的任何名称
+ feature分支（有时也可以被叫做“topic分支”）通常是在开发一项新的软件功能的时候使用，这个分支上的代码变更最终合并回develop分支或者干脆被抛弃掉（例如实验性且效果不好的代码变更）。
+ 一般而言，feature分支代码可以保存在开发者自己的代码库中而不强制提交到主代码库里。


## 五、发布分支

### 基本概念

release分支是为发布新的产品版本而设计的。在这个分支上的代码允许做小的缺陷修正、准备发布版本所需的各项说明信息（版本号、发布时间、编译时间等等）。通过在release分支上进行这些工作可以让develop分支空闲出来以接受新的feature分支上的代码提交，进入新的软件开发迭代周期。

### 啥时候需要release分支

当develop分支上的代码已经包含了所有即将发布的版本中所计划包含的软件功能，并且已通过所有测试时，我们就可以考虑准备创建release分支了。而所有在当前即将发布的版本之外的业务需求一定要确保不能混到release分支之内（避免由此引入一些不可控的系统缺陷）。

### 使用规范：
+ 可以从develop分支派生、使用develop分支作为父分支。
+ 这个分支只应该做bug修复、文档生成和其它面向发布的任务。
+ 发布完成之后，发布分支应该合并到master分支并分配一个版本号打好tag。
+ 从新建发布分支以来的做的修改要合并回develop分支。
+ 分支命名惯例：release-*
+ 当前发布分支名称：release/[release version No.]
+ 当前发布bug修复分支名称：release-bugfix-[Version No.]/[bug name|bug No.]

### release之后

成功的派生了release分支，并被赋予版本号之后，develop分支就可以为“下一个版本”服务了。所谓的“下一个版本”是在当前即将发布的版本之后发布的版本。版本号的命名可以依据项目定义的版本号命名规则进行。


