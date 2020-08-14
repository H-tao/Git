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

### 常用命令

```bash
# 查看帮助
git branch -h			# 终端中输出帮助
git branch --help		# 打开git帮助文档

# 查看remotes/origin下的分支
git branch -r
git ls-remote origin	# 会显示最新的 commit ID

# 查看所有分支，包括heads下和remotes/origin下的
git branch -a

# 切换分支
git checkout <分支名>

# 新建分支，默认以当前分支为基础
git branch <新分支名>

# 新建并切换分支
git checkout -b <新分支名>

# 删除分支，删除的是heads下的分支test
git branch -d test

# 删除remotes/origin下的分支test，并提交到远端(即删除远端的test)
git branch -rd origin/test
git push origin --delete test	# push会同时删除remotes/origin和远端的test

# 提交分支：push分支test到remotes/origin和远端的new_test
git push origin test:new_test

# 重命名分支，重命名的是heads下的分支
git branch -m old_name new_name

# 删除所有名字以 temp 开头的分支（多加两个空格是因为 git branch 输出结果带有空格）
git branch | grep -E "^  temp" | xargs git branch -d
git branch | grep -E "^  temp" | xargs git branch -D	# 强制删除

# 强制删除 master 和当前分支以外的所有分支
git branch | grep -Ev "master" | xargs git branch -D
```

`merge` 默认会将分支与***当前分支***合并。当前分支指的是 `HEAD` 指向的分支，该分支的指向可以在

```bash
# 将origin/master与当前分支合并
git merge origin/master

# 将hotfix分支与当前分支合并，hotfix默认搜索heads/
git merge hotfix
git diff hotfix 	# 查看hotfix与当前分支的不同

# 出现冲突，解决过程
git status -s	# UU 表示出现冲突的文件
vim conflict.*	# 先修改出现冲突的文件
git add .		# add 告诉git冲突已经解决
git status -s	# M 表示冲突已经解决
git commit -m "conflict"	# 提交解决冲突后的新版本
```

`fetch` 默认只将远端更新到remotes/origin，不会更新heads。

```bash
# 将远端更新到remotes/origin，不会更新heads
git fetch
git diff HEAD FETCH_HEAD	

# 获取远端的分支，同步远端的dev分支到 remotes/origin/dev 和 heads/temp
git fetch origin dev:temp
```

`push` 会同时影响 remotes/origin 和远端

```bash
# 提交分支：push分支test到remotes/origin和远端的new_test
git push origin test:new_test

# push会同时删除remotes/origin和远端的test
git push origin --delete test	
```

