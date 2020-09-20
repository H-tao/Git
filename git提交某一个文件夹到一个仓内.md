## 0. 前情提要

自己搞了一个工程，要把整个工程文件夹加到一个现有的Git仓内，这个仓不是我的，是所有人的，我的工程放进去就是其中的一个文件夹。但是先git clone，然后把工程文件夹复制粘贴进去实在是太麻烦，还要重新打开工程才方便继续修改。我不想复制粘贴，怎么搞呢？很简单，直接在工程文件夹里初始化现有的仓，然后添加提交。

## 1. 解决办法

提交到master分支。

```bash
# 初始化
git init

# 配置远程仓地址
git remote add origin git@github.com:H-tao/GitTest.git

# 先拉取远程仓master分支的文件
git pull origin master
# 此时本地仓内会生成一个新的master分支

# add commit push 常规三连操作
git add <工程文件夹>
git commit -m "提交信息"
git push origin master
```

如果你要提交到的不是master分支怎么办呢？比如说我要提交到test_1分支。

```bash
# 初始化
$ git init

# 配置远程仓地址
$ git remote add origin git@github.com:H-tao/GitTest.git

# 先拉取远程仓test_1分支的文件
$ git pull origin test_1
# 此时本地仓内会生成一个新的master分支，但内容都是test_1分支里的。

# 查看所有分支
$ git branch -a
* master
  remotes/origin/test_1

# 切换到test_1
$ git checkout -b test_1
Switched to a new branch 'test_1'

# add commit push 常规三连操作
$ git add <工程文件夹>
$ git commit -m "提交信息"

# 提交这里，明确写出要提交的分支，别搞错了
$ git push origin test_1:test_1
```

## 2. 思考

我在想有没有能够直接追加文件夹的方式push到远程仓，这样就不需要pull同步了。可是这样做会有危险性，因为git不能确定远程仓的信息，如果存在同名的文件夹，就凉凉，所以一定要先pull，再push。因此追加的方式就不能使用。

