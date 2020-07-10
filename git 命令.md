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
git commit	# 把暂存区的修改做一次版本记录


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

