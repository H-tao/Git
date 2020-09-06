### 0. 前情提要

想修改一下我的某个文件/文件夹名字，发现一改，怎么这个文件绿色的 √ 就没了？？？改回来之后，√ 又回来了！！！特么的，咋回事呢？

别急， Git 追踪文件是根据文件名来的，把文件名改了，它就不知道那该死的文件去哪了，它就以为你删掉了！！！所以你在本地直接改名一个文件之后，`git status` 发现的就是 **deleted** 和 **untracked**。但这不是我的本意啊！！！

所以想要修改文件名，我们就需要用到 `git mv` 命令了。

### 1. git mv 详解重命名

重命名文件或文件夹可以使用 `git mv` 命令。参数详解：

`-v`：显示信息。

`-f`：强制重命名或移动，会覆盖目标文件。

`-k`：跳过对重命名或移动出错的文件。出错的时候发生在源文件不存在，或者没有追踪的源文件，或者目标文件已经存在，但没有加`-f`进行覆盖。

`-n`：只显示信息，但不会进行实际重命名或移动操作。

**注意文件状态：**

1. 只能修改已经追踪的文件和文件夹
2. 修改之后，相当于执行了 `add` ，直接 `commit` 就可以提交。

#### 1.1 重命名文件

 `-f` 指强制重命名或移动，注意：**若目标已经存在，则会覆盖目标文件**。

```bash
$ git mv -v oldfile newfile
# $ git mv -f oldfile newfile

# 已经追踪，无需进行 add -u
$ git status
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    oldfile -> newfile

# 重命名之后正常 commit push 就可以了
$ git commit -m "rename oldfile to newfile"
$ git push
```

#### 1.2 重命名文件夹

`/` 不会产生影响。**若 newfolder 文件夹原本已经存在，则会将 oldfolder 移入 newfolder。**

```bash
$ git mv -v oldfolder newfolder
# $ git mv -v oldfolder/ newfolder/

# 已经追踪，无需进行 add -u
$ git status
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    oldfolder/... -> newfolder/...

# 重命名之后正常 commit push 就可以了
$ git commit -m "rename oldfolder to newfolder"
$ git push
```

