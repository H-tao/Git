

# [Git创建空白新分支](https://www.cnblogs.com/wonux/p/5213126.html)

向分支提交一个初始的空commit，保证完全复位。

- 创建并切换新分支

```
git branch <new_branch>
git checkout <new_branch>
git rm --cached -r . 
git clean -f -d
```

- 创建空的commit

```
git commit --allow-empty -m "[empty] initial commit"
```

- 推送新分支

```
git push origin <new_branch>
```



