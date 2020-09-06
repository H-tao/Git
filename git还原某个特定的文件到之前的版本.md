### 0. 前情提要

提交了多个 commit 之后，发现对**某些个文件**修改的不满意或者修改错误，**想把这某些个文件回退到之前的某个版本**，**但是又不想把整个工作区的内容从版本库中全部恢复**。

比如想从版本库中恢复不满意的 `hellopython.py` 文件到工作区：

```
git log hellopython.py
git checkout commitID hellopython.py
git commit -m "hellopython版本回退" hellopython.py
```

### 1. 使用示例

#### 1. git log 查看版本

**commit 关键字后面的一串值为版本号，复制一下自己想回退的版本号**。比如我想将 hellopython.py 回退到 update1，我复制了   e3d77e3be7d0240b5e696999a17940ec8d1b3b82。

```bash
$ git log helloworld.py                                                           
commit 3a74c22e0db4c704a3e72f6518ee77266d6cdd19
Author: Spade_
Date:   Tue Sep 1 20:37:58 2020 +0800

    update3

commit 643267ac028cc14926e91a6c962dd98ee0b1b049
Author: Spade_
Date:   Thu Aug 13 15:29:47 2020 +0800

    update2

commit e3d77e3be7d0240b5e696999a17940ec8d1b3b82
Author: songhaitao WX944363 <songhaitao2@huawei.com>
Date:   Wed Aug 12 16:18:20 2020 +0800

    update1

commit 1306649d2f883e8667296ee723076af04d3f902d
Author: Spade_
Date:   Wed Aug 12 15:44:12 2020 +0800

    2020-08-15 15:44

commit 5fa6aff86d8d4ad5390a78261dbeedc913eabbf5
Author: Spade_
Date:   Fri Jun 19 09:23:59 2020 +0800

    加入执行时间
```

#### 2. git checkout

git checkout 用于从暂存区中恢复文件到工作区。此处我们只想恢复某一个版本的 hellopython.py，只需要 `git checkout commitID 文件名` 就可以了。

```bash
$ git checkout e3d77e3be7d0240b5e696999a17940ec8d1b3b82 helloworld.py
```

恢复回最新版（取消版本回退）的 hellopython.py：

```bash
$ git checkout 3a74c22e0db4c704a3e72f6518ee77266d6cdd19 helloworld.py
```

最后 `git commit` 一下就可以咯。
