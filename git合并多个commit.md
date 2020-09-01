### 0. 背景

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

我想把我改的 commit ID 全部合成一个新的

>8403afe13664d6bb7f5a5557716a030e9389a944		# 我改的
>
>295ac3b842b4ecb6eff1c9954a281a4606a8bc84		# 别人改的



第一种方法：

```bash
git reset --soft 295ac3b842b4ecb6eff1c9954a281a4606a8bc84
git add -u
git commit -m "修改信息"
git push --force
```

需要开启强制合入的选项。

### 1. git log 查看 commit ID

```bash
$ git log
commit 85d5d8fa468b06bb9a62fafde01d80cbb7396682
Author: Spade_
Date:   Tue Sep 1 18:41:44 2020 +0800

    修改5

commit 621ca4121f971d9604e395556763551427d799d9
Author: Spade_
Date:   Tue Sep 1 18:40:39 2020 +0800

    修改4

commit f744d2e91916ab7831f3a7695d1d1825916db164
Author: Spade_
Date:   Mon Aug 31 18:43:52 2020 +0800

    修改3

commit 5c135e49e683563fa470d7f5c281050ec1d73af9
Author: Spade_
Date:   Mon Aug 31 16:55:18 2020 +0800

    修改2

commit 295ac3b842b4ecb6eff1c9954a281a4606a8bc84
Merge: 0830e4c efe0737
Author: Other
Date:   Mon Aug 31 11:56:39 2020 +0800
```

