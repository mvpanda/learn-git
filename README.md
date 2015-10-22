# learn-git
Created at: 2015/10/22 12:00:00   
Copied from: http://www.liaoxuefeng.com/

## 目录
* [1. 初始化](#1)
  * [1.1 put under git](#1.1)
* [2. 时光机](#2)
  * [2.1 版本回退](#2.1)
  * [2.2 工作区和暂存区](#2.2)
  * [2.3 管理修改](#2.3)
* [3. 远程仓库](#3)
  * [3.1 ssh](#3.1)
  * [3.2 操作远程仓库](#3.2)

<a name="1" />
## 1. 初始化
项目+git
<a name="1.1" />
#### 1.1 config

|命令|说明|
|:---|:---|
|git config [--global] [user.name/user.email] "*"|设置（全局）名字和邮箱|
|git init|项目+git|
|git add|可添加文件或目录|
|git commit -m "*" [file/dir,...]|提交|


<a name="2" />
## 2. 时光机
版本操作相关

<a name="2.1" />
#### 2.1 版本回退

|命令|说明|
|:---|:---|
|git log|穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。|
|git reflog|要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。|
|git reset [--hard] [commit_id\|HEAD^\|HEAD^^\|HEAD~5\]|`HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用该命令。当使用`--hard`时，指定版本库；当不使用`--hard`时，指定暂存区|

<a name="2.2" />
#### 2.2 工作区和暂存区

__工作区（Working Directory）__   
本地文件目录

__版本库（Repository）__   
`.git`是Git的版本库。Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区。
  
![图片]()

<a name="2.3" />
#### 2.3 管理修改

__git add->git commit__   
每次修改，如果不add到暂存区，那就不会加入到commit中   

__git rm__   
`git rm`或者`rm`删除文件。   

__git diff__   
1. `git diff`：是查看working tree与index file的差别的。   
1. `git diff --cached`：是查看index file与commit的差别的。   
1. `git diff HEAD`：是查看working tree和commit的差别的。（你一定没有忘记，HEAD代表的是最近的一次commit的信息）   

__git checkout file...__   
命令`git checkout -- readme.txt`意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：   
  * readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；   
  * readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到刚添加到暂存区后的状态。   
总之，就是使这个文件的工作区状态和暂存区一致。   
>`git checkout -- file`命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令   

__git reset HEAD file__   
用命令`git reset HEAD file`可以把暂存区的修改撤销掉（unstage），重新放回工作区。当我们用`HEAD`时，表示最新的版本。   

<a name="3" />
## 3. 远程仓库
远程仓库相关

<a name="3.1" />
#### 3.1 ssh

1. 创建ssh-key   
> $ ssh-keygen -t rsa -C "youremail@example.com"   
1. 登陆GitHub，打开“Account settings”，“SSH Keys”页面，然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容。   

_ref:https://help.github.com/articles/generating-ssh-keys/_

>另一种方式remote.origin.url=https://username:passwd@github.com/username/project.git   

<a name="3.2" />
#### 3.2 操作远程仓库

要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；   
关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。   
此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；   

要克隆一个远程库，使用命令`git clone repo_url`
