# git的使用

## 安装好Git后，在命令行输入：

``` git config --global user.name "1097017225"   ```           //指定用户名

``` git config --global user.email "1097017225@qq.com" ```     //指定邮箱

因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址
git init //初始化当前目录为创库所在目录

## 新建一个目录，通过git init命令把这个目录变成Git可以管理的仓库
``` git init ```                                   //初始化当前目录为创库所在目录

## 添加文件到本地创库
``` git add test.cpp ```                   //添加文件到暂存区

``` git commit -m "提交描述" ```            //提交到本地创库

每次修改文件后都要add和commit一次
```git diff```  //查看修改的内容
运行git status命令看看结果：

``` git stataus ``` 

```

On branch master

Your branch is up to date with 'origin/master'.

Changes not staged for commit:

  (use "git add <file>..." to update what will be committed)

  (use "git checkout -- <file>..." to discard changes in working directory)


        modified:   test.cpp


no changes added to commit (use "git add" and/or "git commit -a")
```

git status命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，test.cpp被修改过了，但还没有准备提交的修改

## 在Git中，删除也是一个修改操作
``` rm test.app ```                  //删除工作区里的文件

``` git rm test.app ```             //删除版本库里的文件

``` git commit -m "删除文件" ```     //确认删除文件

如果用rm命令删除错了，可以用：

```git checkout -- test.cpp  ``` //用版本库里的版本替换工作区的版本

## 版本回退
用git log命令可以查看最近到最远的提交日志
``` git log ``` //命令显示从最近到最远的提交日志 加上--pretty=oneline 简化输出

回退到上一个版本：

``` git reset --hard HEAD^  ``` //回退到上一个提交的版本 HEAD^^表示上两个版本

如果回退后想要恢复：

``` git reflog ``` //用来记录你的每一次命令，找到回退的HEAD号
查看工作区和版本库里面最新版本的区别：
``` git diff HEAD -- readme.txt ``` //查看工作区和版本库里面最新版本的区别


## 撤销修改 
修改文件后需要撤销掉之前的修改内容：

```git checkout -- readme.txt ``` //把readme.txt文件在工作区的修改全部撤销 

一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态

一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态

git reset HEAD <file> //把暂存区的修改撤销掉，重新放回工作区,相当于回到修改工作区文件后未add的状态


## 怎么管理远程创库

每次用：

``` git clone git@github.com:1097017225/1097017225.github.io.git ```

克隆下来后远程创库会自动和本地创库关联起来 

创建分支：

``` git checkout -b dev ```  //创建并切换到dev分支
上面一步可以用下面两步组成：
```git branch dev ```    //创建分支

```git checkout dev ```  //切换分支    ，这两步和上面那一步效果一样
查看当前所有的分支：

```git branch ``` // 列出所有分支，前分支前面会标一个*号

把分支和主分支融合：

``` git merge dev  ```//合并分支内容，合并之前切换到主分支
融合后删除分支：

```git branch -d dev ``` //删除分支



把本地创建的分支并提交到远程库

``` git push origin dev ``` 

git clone克隆的时候只能把主分支克隆下来，但是可以查看远程创库的分支：


``` git branch -r ``` 

``` git branch -a ```   // 查看所有分支，本地创库和远程创库

从远程库拉取分支：

``` git fetch origin 远程分支:本地分支 ```

采用此种方法建立的本地分支不会和远程分支建立映射关系,提交的时候分支要单独提交

``` git checkout -b 本地分支 origin/远程分支 ```//拉取远程分支，并和本地创建的分支关联起来

最后所有的提交都用：
``` git push ```
