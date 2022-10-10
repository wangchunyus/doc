## Git-安装说明（Mac）

指引地址: [https://blog.csdn.net/rockvine/article/details/122898165](https://blog.csdn.net/rockvine/article/details/122898165)



## Git-本地操作命令

+ **git init**
  + 通过git init命令把这个目录变成Git可以管理的仓库。
+ **git add red.txt**
  - 把文件添加到仓库
+ **git commit -m '本次提交的说明'**
  - 把文件提交到仓库  -m是本次提交的说明。
+ **git status**
  - 查看文件状态 ，如果修改某个文件后 使用此命令，会提示 某些文件被修改了。
+ **git reset HEAD  文件名** 
  + 可以将文件从暂存区的修改撤销到工作区。
+ **git checkout - 文件名**
  + 可以丢弃工作区的修改。

## Git-区域划分说明

+ **区域**

  + **工作区**

    + 在电脑中能看到的目录，比如 一个名字为work的文件夹就是一个工作区。
  + **版本库**
  + 工作区中有一个 隐藏目录 ‘.git’ 这个不属于工作区 而是git版本库。
  
  + **暂存区**
  
    + 版本库中的 stage 或者叫做（index）属于暂存区域。


## Git-远程仓库配置使用

+ **创建 SSH KEY 命令**
  + ssh-keygen -t rsa -C  “你的邮箱地址”

+ **添加远程仓库 命令**

  + 1.在本地已经有一个git仓库了，又想要在github创建一个git仓库，并且向让俩仓库远程同步，首先登录github创建一个新仓库。

  + 2.命令：git remote add origin git@github.com:wangchunyus/learngit.git关联本地库其中origin为远程库名可任意取，后面 xwangchunyus替换为你自己的github账户名

  + 3.命令git push -u origin master本地库的所有内容推送到远程库，实际上是把当前分支master推送到远程。

  + 4.命令 git push origin master 推送最新修改。

    









