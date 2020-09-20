### 0. 前情提要

要准备提交MR了，改了半天搞了很多个commit，都push上去了，但是提交MR的时候要合成一个commit，咋搞呢？

#### 0.1 我期望的效果

##### 1. 合并commit之前

比如我现在有4个 commit ID，从新到旧分别为

> 85d5d8fa468b06bb9a62fafde01d80cbb7396682		# 我改的
>
> 621ca4121f971d9604e395556763551427d799d9		# 我改的
>
> f744d2e91916ab7831f3a7695d1d1825916db164		# 我改的
>
> 5c135e49e683563fa470d7f5c281050ec1d73af9		# 我改的
>
> 295ac3b842b4ecb6eff1c9954a281a4606a8bc84		# 别人改的

##### 2. 合并commit之后

我想把我改的 commit ID 全部合成一个新的 commit ID 

>8403afe13664d6bb7f5a5557716a030e9389a944		# 我改的
>
>295ac3b842b4ecb6eff1c9954a281a4606a8bc84		# 别人改的

### 1. 合并commitID的方法

#### 1.1 第一种方法：先从版本库回退内容到暂存区，再重新提交工作区的内容

思路：使用 git reset --soft 回退版本库和暂存区的版本，同时保留工作区的变动，之后再重新提交工作区的内容就好了。

```bash
# 查看前10个commit
git log -10
# 从版本库恢复文件到暂存区，不改动工作区的内容
git reset --soft 295ac3b842b4ecb6eff1c9954a281a4606a8bc84	# 别人改的commitID
# add已经跟踪的文件
git add -u
# 提交
git commit -m "修改信息"
# 强制push以替换远程仓的commitID
git push --force
```

如果push失败，出现Reject，需要开启强制合入的选项。

> **Settings -> Repository -> Protected Branches -> Protected branch （找到分支） -> Unprotect**

#### 1.2 第二种方法：git rebase

git rebase 会临时创建一个新分支进行，**如果出错了**，可以 `git checkout 原分支名` 之后重新 git rebase。

pick：使用commit。

reword：使用commit，修改commit信息。

squash：使用commit，将commit信息合入上一个commit

fixup：使用commit，丢弃commit信息。

```bash
# 查看前10个commit
git log -10
# 将4个commit压缩成一个commit
git rebase -i HEAD~4	
# add已经跟踪的文件
git add -u
# 提交
git commit -m "修改信息"
# 强制push以替换远程仓的commitID
git push --force
```





<https://blog.csdn.net/Al_assad/article/details/81145856> 

