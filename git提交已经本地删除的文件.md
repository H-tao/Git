# git commit deleted

git status下，查看有deleted文件

用git rm 会报错，did not match any files，提示没有此文件。

```
git add -u

git commit -m "commit deleted files"
```

 

```bash
sWX944363@Y00464117 ~/Desktop/Projects/codequalityspider (master)
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   settings.py

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    "CloudPipeline_CodeQuality-\344\277\241\346\201\257\346\225\264\345\220\210.xlsx"
        deleted:    CloudPipeline_CodeQuality.xlsx
        deleted:    "NFV_FusionStage_21.0.0.B090\346\236\204\345\273\272\344\275\277\347\224\250\347\232\204\345\205\250\351\207\217\344\273\243\347\240\201\344\273\223.xlsx"
        deleted:    "PaaS\350\264\250\351\207\217\347\273\237\350\256\241\346\225\260\346\215\256\346\240\274\345\274\217.xlsx"

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .idea/
        "PaaS\350\264\250\351\207\217\347\273\237\350\256\241\346\225\260\346\215\256_2020-07-21 160614.xlsx"
        __pycache__/


sWX944363@Y00464117 ~/Desktop/Projects/codequalityspider (master)
$ git add -u

sWX944363@Y00464117 ~/Desktop/Projects/codequalityspider (master)
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    "CloudPipeline_CodeQuality-\344\277\241\346\201\257\346\225\264\345\220\210.xlsx"
        deleted:    CloudPipeline_CodeQuality.xlsx
        deleted:    "NFV_FusionStage_21.0.0.B090\346\236\204\345\273\272\344\275\277\347\224\250\347\232\204\345\205\250\351\207\217\344\273\243\347\240\201\344\273\223.xlsx"
        deleted:    "PaaS\350\264\250\351\207\217\347\273\237\350\256\241\346\225\260\346\215\256\346\240\274\345\274\217.xlsx"
        modified:   settings.py

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .idea/
        "PaaS\350\264\250\351\207\217\347\273\237\350\256\241\346\225\260\346\215\256_2020-07-21 160614.xlsx"
        __pycache__/


sWX944363@Y00464117 ~/Desktop/Projects/codequalityspider (master)
$ git commit -m "deleted"
[master 5f81867] deleted
 5 files changed, 3 insertions(+), 40 deletions(-)
 delete mode 100644 "CloudPipeline_CodeQuality-\344\277\241\346\201\257\346\225\264\345\220\210.xlsx"
 delete mode 100644 CloudPipeline_CodeQuality.xlsx
 delete mode 100644 "NFV_FusionStage_21.0.0.B090\346\236\204\345\273\272\344\275\277\347\224\250\347\232\204\345\205\250\351\207\217\344\273\243\347\240\201\344\273\223.xlsx"
 delete mode 100644 "PaaS\350\264\250\351\207\217\347\273\237\350\256\241\346\225\260\346\215\256\346\240\274\345\274\217.xlsx"

sWX944363@Y00464117 ~/Desktop/Projects/codequalityspider (master)
$ git push
warning: push.default is unset; its implicit value is changing in
Git 2.0 from 'matching' to 'simple'. To squelch this message
and maintain the current behavior after the default changes, use:

  git config --global push.default matching

To squelch this message and adopt the new behavior now, use:

  git config --global push.default simple

When push.default is set to 'matching', git will push local branches
to the remote branches that already exist with the same name.

In Git 2.0, Git will default to the more conservative 'simple'
behavior, which only pushes the current branch to the corresponding
remote branch that 'git pull' uses to update the current branch.

See 'git help config' and search for 'push.default' for further information.
(the 'simple' mode was introduced in Git 1.7.11. Use the similar mode
'current' instead of 'simple' if you sometimes use older versions of Git)

Counting objects: 5, done.
Delta compression using up to 12 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 310 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Start Git Hooks Checking                                        [PASSED]
To ssh://git@gitlab.huawei.com:2222/sWX944363/codequalityspider.git
   5fbb75e..5f81867  master -> master
```

