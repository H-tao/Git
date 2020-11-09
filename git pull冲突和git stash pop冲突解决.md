

## 一、git pull 冲突

代码仓有人提交了新代码，而我本地也修改了代码，想要pull一下，却发现：

```
error: Your local changes to the following files would be overwritten by merge:
        xxx.xxx
Please, commit your changes or stash them before you can merge.
```

百度了一下解决办法很简单，有两种：

1. **暂存本地的修改，pull之后解决冲突**
2. 撤销本地所有的修改，再pull

### 第一种办法：**暂存本地的修改，pull之后解决冲突**

```bash
git stash
git pull
git stash pop
```

如果 git stash pop 遇见冲突，请见后文 `git stash pop 冲突`。

### 第二种办法：撤销本地所有的修改

```bash
git reset --hard
git pull
```

## 二、git stash pop 冲突

git stash和git pull之后，想要git stash pop，却报错：

```
error: Your local changes to the following files would be overwritten by merge:
        xxx.xxx
Please, commit your changes or stash them before you can merge.
```

报错原因：对 git pull 之后的代码有修改。

```bash
$ git status
	...
        modified:   test.txt
        modified:   work/workspace.xml
        modified:   work/ssss
        modified:   work/aaa
		...

$ git checkout .	# 撤销git pull之后的所有修改
# $ git checkout -- test.txt	 # 撤销test.txt的修改
# $ git checkout -- work/		 # 撤销work/目录下所有文件的修改


$ git statsh pop
Auto-merging user/views.py
CONFLICT (content): Merge conflict in user/views.py
The stash entry is kept in case you need it again.
```

