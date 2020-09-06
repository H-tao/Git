## 版本管理

```bash
# 创建版本库
git init


# 版本创建
git add
git commit -m "版本说明信息"


# 查看版本记录
git log


# 版本回溯，HEAD^指向当前版本的前一版本
git reset --hard HEAD^


# 查看操作记录
git reflog


# 工作区，版本库和暂存区
git add		# 把工作区的修改放入暂存区
git add -u	# 只add已经追踪过的文件
git commit -m "修改信息"	# 把暂存区的修改做一次版本记录


# 撤销修改
1. 撤销工作区的修改
git checkout -- <file>

2. 撤销已经add到暂存区，但未commit的修改
git reset HEAD <file>
+
# git checkout -- <file>	# 注意，这会将工作区的修改也撤销，如果不希望撤销工作区的修改则不必使用

3. 已经commit，版本回退至前一版本

# 1.git reset --soft 版本号 
# 不删除工作区改动的代码，撤销commit，不撤销git add .
git reset --soft HEAD^  //回到上一个版本


# 2.git reset --mixed 版本号 
# 不删除工作区改动的代码，撤销commit，撤销git add .
git reset --mixed HEAD^  //回到上一个版本


# 3.git reset --hard 版本号 
# 删除工作区的代码，撤销commit，撤销git add . 回到上一次commit的状态
git reset --hard HEAD^  # 慎用此命令，因为会将工作区的文件也一并修改掉


# 对比工作区和版本库文件的不同
[root@i hellogit]# git diff HEAD -- code.py 
diff --git a/code.py b/code.py
index 8ebeb35..61ef177 100644
--- a/code.py	# -代表版本库
+++ b/code.py	# +代表工作区
@@ -1 +1,2 @@
 1. This is a code py
+2. This for git add and git checkout -- file	# 出现+号，说明工作区比HEAD版本多了一行

# 对比两个版本库文件的不同
## 
[root@i hellogit]# git diff HEAD HEAD^ -- code.py 
diff --git a/code.py b/code.py
index 61ef177..8ebeb35 100644
--- a/code.py	# -代表当前版本
+++ b/code.py	# +代表后一个版本
@@ -1,2 +1 @@
 1. This is a code py
-2. This for git add and git checkout -- file	# 当前版本比后一个版本多一行

[root@i hellogit]# git diff HEAD^ HEAD -- code.py 
diff --git a/code.py b/code.py
index 8ebeb35..61ef177 100644
--- a/code.py	# -代表后一个版本
+++ b/code.py	# +代表当前版本
@@ -1 +1,2 @@
 1. This is a code py
+2. This for git add and git checkout -- file	# 当前版本比后一个版本多一行


# 删除文件
见git-rm命令

```

## 分支管理

```bash

```

### git clone 命令

我们使用 **git clone** 从现有 Git 仓库中拷贝项目（类似 **svn checkout**）。

克隆仓库的命令格式为：

```
git clone <repo>
```

如果我们需要克隆到指定的目录，可以使用以下命令格式：

```
git clone <repo> <directory>
```

**参数说明：**

- **repo:**Git 仓库。
- **directory:**本地目录。

比如，要克隆 Ruby 语言的 Git 代码仓库 Grit，可以用下面的命令：

```
$ git clone git://github.com/schacon/grit.git
```

执行该命令后，会在当前目录下创建一个名为grit的目录，其中包含一个 .git 的目录，用于保存下载下来的所有版本记录。

如果要自己定义要新建的项目目录名称，可以在上面的命令末尾指定新的名字：

```
$ git clone git://github.com/schacon/grit.git mygrit
```

git clone 时，可以所用不同的协议，包括 ssh, git, https 等，其中最常用的是 ssh，因为速度较快，还可以配置公钥免输入密码。各种写法如下：

```bash
git clone git@github.com:fsliurujie/test.git         --SSH协议
git clone git://github.com/fsliurujie/test.git          --GIT协议
git clone https://github.com/fsliurujie/test.git      --HTTPS协议
```

### git config 命令

1.仓库级别 local。 

2.用户级别 global。

3.系统级别 system。 

```bash
git config --local
git config --global
git config --system
```

三级目录：

```bash
~/project/.git/config # 项目仓库目录，对应 local 级别
~/.gitconfig    # 当前用户目录，对应 global 级别
/etc/gitconfig  # git安装目录，对应 system 级别
```

### git diff

执行 git diff 来查看执行 git status 的结果的详细信息。

git diff 命令显示已写入缓存与已修改但尚未写入缓存的改动的区别。git diff 有两个主要的应用场景。

- 尚未缓存的改动：**git diff**
- 查看已缓存的改动： **git diff --cached**
- 查看已缓存的与未缓存的所有改动：**git diff HEAD**
- 显示摘要而非整个 diff：**git diff --stat**

```bash
# git diff <local branch> <remote>/<remote branch>　
# 显示本地 master 分支和 远程 master 分支文件改动的摘要
git diff --stat master origin/master  
```

**简单示例： **

```bash
# 新建一个文件
[banana@CentOS7 hellopython]$ vim test2
# 添加一行内容：
This is a Test File


# 查看状态
[banana@CentOS7 hellopython]$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   helloworld.py		` 已经修改但未缓存( add ) 的文件 `

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	1.sh
	test2
	
no changes added to commit (use "git add" and/or "git commit -a")


# 将 test2 加入暂存区，并查看状态
[banana@CentOS7 hellopython]$ git add test2 
[banana@CentOS7 hellopython]$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   test2              ` 添加到·缓存区的新文件 `

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   helloworld.py      ` 已经修改但未缓存( add ) 的文件 `

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	1.sh
	

# 查看已缓存的改动： git diff --cached
[banana@CentOS7 hellopython]$ git diff --cached
diff --git a/test2 b/test2
new file mode 100644
index 0000000..71d030c
--- /dev/null
+++ b/test2
@@ -0,0 +1 @@
+This is a Test File


# 尚未缓存的改动：git diff
[banana@CentOS7 hellopython]$ git diff
diff --git a/helloworld.py b/helloworld.py
index 407c194..e601cf4 100644
--- a/helloworld.py
+++ b/helloworld.py
@@ -1,2 +1,3 @@
 import datetime
 print(datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S"), "    Hello World!")
+print("This is a HelloWorld python file")


# 查看已缓存的与未缓存的所有改动：git diff HEAD
[banana@CentOS7 hellopython]$ git diff HEAD
diff --git a/helloworld.py b/helloworld.py
index 407c194..e601cf4 100644
--- a/helloworld.py
+++ b/helloworld.py
@@ -1,2 +1,3 @@
 import datetime
 print(datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S"), "    Hello World!")
+print("This is a HelloWorld python file")
diff --git a/test2 b/test2
new file mode 100644
index 0000000..71d030c
--- /dev/null
+++ b/test2
@@ -0,0 +1 @@
+This is a Test File


# 显示摘要而非整个 diff
[banana@CentOS7 hellopython]$ git diff --stat
 helloworld.py | 1 +
 1 file changed, 1 insertion(+)
 
# 显示摘要而非整个 diff 
[banana@CentOS7 hellopython]$ git diff --cached --stat
 test2 | 1 +
 1 file changed, 1 insertion(+)
```

### git rm

#### 删除本地和远端的文件

> rm <file> / rm -r <dir>
>
> git commit
>
> git push

```bash
# 删除本地文件
[root@CentOS7 hellopython]# rm t1.json 
[root@CentOS7 hellopython]# rm t2.xml 
[root@CentOS7 hellopython]# ls
helloworld.py  README.md


# 查看状态
[root@CentOS7 hellopython]# git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    t2.xml
	deleted:    t1.json

no changes added to commit (use "git add" and/or "git commit -a")


# git commit 提交删除信息
[root@CentOS7 hellopython]# git commit -m "删除自定义的t1.json和t2.xml" ./
[master 2df524d] 删除自定义的t1.json和t2.xml
 2 files changed, 3 deletions(-)
 delete mode 100644 t2.xml
 delete mode 100644 t1.json
 
 
# git push 将删除信息提交到远端
[root@CentOS7 hellopython]# git push
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
..
   4673d12..2df524d  master -> master

```



#### 删除add的文件

> git rm --cached <file>

```bash
# 查看状态
[root@CentOS7 hellopython]# git status
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   build/log/build.log
	new file:   build/nohup.out


# 进行删除
[root@CentOS7 hellopython]# git rm --cached build/nohup.out
rm 'build/nohup.out'
[root@CentOS7 hellopython]# git rm --cached build/log/build.log
rm 'build/log/build.log'


# 删除之后，文件变成Untracked
[root@CentOS7 hellopython]# git status
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	build/log/
	build/nohup.out

```

#### 删除add的文件夹

> git rm -r --cached <dir>

```bash
# 查看状态
[root@CentOS7 hellopython]# git status
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   config


# 删除文件夹
[root@CentOS7 hellopython]# git rm -r --cached config
rm 'config'


# 删除之后，文件夹变成untracked
[root@CentOS7 hellopython]# git status
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	config/
```



### git shh-key的配置

Linux和Windows都适用

```bash
https://blog.csdn.net/felicity294250051/article/details/53606158

# 进入.ssh隐藏文件夹
[root@CentOS7 project]# cd ~/.ssh


# 查看是否已经创建了SSH key
[root@CentOS7 .ssh]# ls


# 生成密钥，后面直接生成
## -t 指定密钥类型，默认是 rsa ，可以省略。
## -C 设置注释文字，比如邮箱。
## -f 指定密钥文件存储文件名。
[root@CentOS7 .ssh]# ssh-keygen -t rsa -C "Coder@github.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/root/.ssh/id_rsa): 	# 直接回车
Enter passphrase (empty for no passphrase): 					# 直接回车
Enter same passphrase again: 									# 直接回车
Your identification has been saved in /home/root/.ssh/id_rsa.
Your public key has been saved in /home/root/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:... Coder@github.com
The key's randomart image is:
+---[RSA 2048]----+
|                 |
|         .       |
|        o .+     |
...
|         E o+ +o |
|        .    +.  |
+----[SHA256]-----+



# 查看生成的密钥
[root@CentOS7 .ssh]# ls
id_rsa  id_rsa.pub


# 确保启用SSH代理
[root@CentOS7 .ssh]# eval "$(ssh-agent -s)"
Agent pid 17744


# 为SSH key启用SSH代理
[root@CentOS7 .ssh]# ssh-add ~/.ssh/id_rsa
Identity added: /home/root/.ssh/id_rsa (/home/root/.ssh/id_rsa)



# 将公钥内容拷贝到Git上的SSH key中
[root@CentOS7 .ssh]# cat id_rsa.pub 
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDBWculElznat8NWr2oPhnLbRm67sJG24z90UU577znLeJF/...3Rd1vOlkDzBd0f0yEqdWxhdNFq33P2HS4ksMCbh+Wl8rhh4yE9gDXJn0xMPjO9KDQvxpCigcJ Coder@github.com

```

### git tag

#### 查看本地分支标签

```bash
git tag

或者

git tag -l

或者

git tag --list
```

#### 查看远程所有标签

```bash
git ls-remote --tags

或者

git ls-remote --tag
```

#### 给当前分支打标签

```bash
git tag 《标签名》

例如

git tag v1.1.0
```

#### 给特定的某个commit版本打标签

比如现在某次提交的id为 039bf8b

```bash
git tag v1.0.0 039bf8b

或者可以添加注释

git tag v1.0.0 -m "add tags information" 039bf8b

或者

git tag v1.0.0 039bf8b -m "add tags information"
```

#### 删除本地某个标签

```bash
git tag --delete v1.0.0

或者

git tag -d v1.0.0

或者

git tag --d v1.0.0
```

#### 删除远程的某个标签

```bash
git push -d origin v1.0.0

或者

git push --delete origin v1.0.0

或者

git push origin -d v1.0.0

或者

git push origin --delete v1.0.0

或者

git push origin :v1.0.0

#### 将本地标签一次性推送到远程/远程标签拉取到本地

git push/pull origin --tags

或者

git push/pull origin --tag

或者

git push/pull --tags

或者

git push/pull --tag
```

#### 将本地某个特定标签推送到远程

```bash
git push origin v1.0.0
查看某一个标签的提交信息

git show v1.0.0
只要把以上几个命令弄熟练了，平时发布版本后想打标签基本可以说是手到擒来了。

根据某个commit创建本地分支

例如: 当前分支的某个commit id = 12345678，我们可以基于这个id创建本地分支

git checkout 12345678 -b newBranch
```

### git 冲突的解决

#### 解决合并冲突

　　第一步：在<<<<<<< <分支名>   ========   >>>>>>>><分支名> 删掉，冲突代码自行合并修改

　　第二部：git add <已修改冲突文件>

　　第三部：git commit -m "合并日志"

　　　　**注意：这里commit提交时不能带上文件**

　　　　**分支名由（first|MERGING）变成（first）说明合并成功**

#### mergetool的使用

### git 分支管理

```bash
Production分支（主线分支用于发版，不会直接改）
Master分支，这个分支只能从其他分支合并，不能在这个分支直接修改
 
Develop分支（开发分支）
这个分支是我们是我们的主开发分支，包含所有要发布到下一个Release的代码，这个主要合并与其他分支，比如Feature分支
 
Feature分支（新功能分支）
这个分支主要是用来开发一个新的功能，一旦开发完成，我们合并回Develop分支进入下一个Release 
 
Release分支（偏向测试）
当你需要一个发布一个新Release的时候，我们基于Develop分支创建一个Release分支，完成Release后，我们合并到Master和Develop分支
 
Hotfix分支（紧急bug发布）
当我们在Production发现新的Bug时候，我们需要创建一个Hotfix, 完成Hotfix后，我们合并回Master和Develop分支，所以Hotfix的改动会进入下一个Release
```

```bash
# git diff <local branch> <remote>/<remote branch>　
# 显示本地 master 分支和 远程 master 分支文件改动的摘要
git diff --stat master origin/master  
```

### Git中文件的4种状态

git库所在的文件夹中的文件大致有4种状态

- Untracked: 未跟踪, 此文件在文件夹中, 但并没有加入到git库, 不参与版本控制. 通过git add 状态变为Staged.
- Unmodify: 文件已经入库, 未修改, 即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为Modified. 如果使用git rm移出版本库, 则成为Untracked文件
- Modified: 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过git add可进入暂存staged状态, 使用git checkout 则丢弃修改过, 返回到unmodify状态, 这个git checkout即从库中取出文件, 覆盖当前修改
- Staged: 暂存状态. 执行git commit则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为Unmodify状态. 执行git reset HEAD filename取消暂存, 文件状态为Modified

### 51个 git 命令

#### 0x0 前言

> 如今，Git 大行其道，颇有一统天下之势。
> 如果你的技能树上 Git 和 Github 的图标还没有点亮的话，你都不好意思说你是程序员。

#### 0x1 54个命令助你乾坤大挪移

###### 1: init ⭐

###### 2: config ⭐

###### 3: add ⭐

###### 4: commit ⭐

###### 5: clone ⭐

###### 6: clone_to_folder ⭐

###### 7: ignore ？？.git

###### 8: include ？？

###### 9: status ⭐

###### 10: number_of_files_committed

###### 11: rm ⭐

###### 12: rm_cached ⭐

###### 13: stash

###### 14: rename

###### 15: restructure

###### 16: log、reflog⭐

###### 17: tag

###### 18: push_tags

###### 19: commit_amend

###### 20: commit_in_future

###### 21: reset

###### 22: reset_soft

###### 23: checkout_file

###### 24: remote

###### 25: remote_url

###### 26: pull

###### 27: remote_add

###### 28: push

###### 29: diff ⭐

###### 30: blame

###### 31: branch

###### 32: checkout

###### 33: checkout_tag

###### 34: checkout_tag_over_branch

###### 35: branch_at

###### 36: delete_branch

###### 37: push_branch

###### 38: merge

###### 39: fetch

###### 40: rebase

###### 41: repack

###### 42: cherry-pick

###### 43: grep

###### 44: rename_commit

###### 45: squash

###### 46: merge_squash

###### 47: reorder

###### 48: bisect

###### 49: stage_lines

###### 50: find_old_branch

###### 51: revert

###### 52: restore

###### 53: conflict

###### 54: submodule

###### 55: contribute

#### 0x2 屌丝训练工具之Git木人巷--githug

```
sudo gem install githug
```

安装成功后，在 Terminal 里进入你常用的目录，输入`githug`，会提示游戏目录不存在，是否要创建一个，输入`y`然后回车：
根据提示`cd git_hug` 进入游戏目录，准备开始游戏。
