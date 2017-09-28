##  gitlab和github一起使用

> [左鹏飞](https://github.com/zuopf769) 2017.09.28

### 1. 背景

通常公司用gitlab来做代码的版本管理和协同开发；而我们有个人的github账号。那咋样才能在一台电脑上同时使用gitlab和github呢？

### 2. 操作步骤

#### 2.1 首先都已经注册了gitlab和github的账户

#### 2.2 生成公钥、秘钥

ssh-keygen -t rsa -C "注册的gitlab邮箱"

名称输入gitlab_id_rsa

ssh-keygen -t rsa -C "注册的github邮箱"

名称输入github_id_rsa

除了名称外，其他一路回车。

完成后会在~/.ssh/目录下生成以下文件:

+ github_id_rsa
+ github_id_rsa.pub
+ gitlab_id_rsa
+ gitlab_id_rsa.pub


#### 2.3 将两个pub文件分别配置到github和gitlab的sshkey中


#### 2.4 编写config文件,告诉本地git到不同的托管平台带不同的钥匙。

```
cd ~/.ssh
vi config
```


config内容如下:

```

#gitlab
Host gitlab
        HostName gitlab.*.com
        IdentityFile ~/.ssh/gitlab_id_rsa

#github
Host github
        HostName github.com
        IdentityFile ~/.ssh/github_id_rsa

```

+ Host可以使用通配符，当ssh的时候如果server的URL能match上这里Host指定的值，则Host下面指定的HostName将被作为最终URL使用。同时该Host下配置的User, Port都将被使用。

+ ssh的server的URL如下图所示

![](https://github.com/zuopf769/how_to_use_git/blob/master/images/gitconfig.jpeg)

+ HostName根据自己实际需求来定


#### 2.5 配置仓库

```
github工作仓库:~/workspace/github
gitlab工作仓库:~/workspace/gitlab

```

```
#gitlab
cd ~/workspace/gitlab
git init
git config --global user.name 'personal'
git config --global user.email 'personal@company.com'

```

```
#github
cd ~/workspace/github
git init
git config --local user.name 'kingboy'
git config --local user.email 'kingboy@163.com'

```

> 注意
> 
> + 把工作用的gitlab的git config配置设置成全局的
> + github的git config配置设置成本地


#### 2.6 接下来在两个目录下新建或者clone项目开发即可.


### 3 参考资料

+ [ssh config配置](http://www.xuebuyuan.com/414672.html)

