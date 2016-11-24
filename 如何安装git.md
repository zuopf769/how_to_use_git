## 如何安装git

### 配置账号

1. 安装 [git客户端](http://www.git-scm.com/download/)，生成`ssh-key`，如:

```
git config --global user.email 用户名@xx.com    # 邮箱
git config --global user.name 用户名
```

2. 配置密码（SSH公钥）；注意：一个key不能被同时添加到多人的github账号下

```
#1）生成密钥，一路回车、用默认选项
ssh-keygen -t rsa -C "你的邮箱"
 
#2）复制到粘贴板
cat ~/.ssh/id_rsa.pub | clip    # Windows
cat ~/.ssh/id_rsa.pub | pbcopy  # MacOS
 
#3）粘贴到github，在github右上角>个人设置>添加SSH Keys[注意：一定要把不可见的换行符去掉]
```

3. 配置命令行提示【非必须】；仅限Linux bash，Mac或Windows安装上文“安装方法”中推荐的客户端后就自动配置好了

```
#一键配置：
#1) 自动补全：https://github.com/git/git/tree/master/contrib/completion
#2) 命令行提示符：https://github.com/xtrementl/dev-bash-git-ps1
```

4. 编写代码

使用`git clone git@github.com:zuopf769/how-to-use-git.git`克隆出项目后，可修改，完成后可提交并推送，如：

```
git clone git@github.com:zuopf769/how-to-use-git.git
cd XX
vim readme.md
...
git add -A
git commit -m '更新说明'
git push
```

当推送（`push`）后，网站会自动更新为最新内容。

> ps: 修改前最好`git pull`更新下，以防冲突，[git简单使用说明](http://www.bootcss.com/p/git-guide/)











