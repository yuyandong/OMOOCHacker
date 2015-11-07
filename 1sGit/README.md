# Git & GitHub
~ 上手、使用的心得体会

.git 

`git commit -am "xxx"` -am _add + commit 

`git diff` 会返回本地仓库和远程仓库的文件的不同。比如默认使用vim 打开 文本文件。

`git merge-file `
>A conflict occurs if both <current-file> and <other-file> have changes in a common segment of lines. If a conflict is found, git merge-file normally outputs a warning and brackets the conflict with lines containing <<<<<<<and>>>>>>> markers. A typical conflict will look like this:

`<<<<<<< A
lines in file A
=======
lines in file B
>>>>>>> B`

## 进展

- 151029 Created

##疑问和尝试解

>本周的作业内容:
>Fork OMOOCHacker 仓库
>未完成仓库 fork 的同学请尽快呐~
>将仓库中 1sGit 文件夹下的 4 个 Version.doc 文件, 依版本顺序合并为一个文件
对此作业要求有 2 个小疑问。自问自答，还是没有解决，故在此提出疑问`Q`  和所尝试 `A` 。

### 疑问 1 

-  Q 1 : `依版本顺序合并` 是怎么个形式？我不明白 "依版本顺序合并" 所指...

> 将仓库中 1sGit 文件夹下的 4 个 Version.doc 文件, 依版本顺序合并为一个文件

- A 1 : 难道是删除 ？ 用 page 修改 v1.0-->v1.1--->v2.0--->v2.1 ? 

然后 `git commit -am "combines to Version2.1.doc" `  + `git push`  打完收工 ?


*PS 0 : 如果是这般做法， **合并** 何在？*


### 疑问 2

- Q 2 : 命令行中使用`git merge-file` 命令合并 四个文件为一个？

- A 2 : 因为 `git clone`  fork到本地的库没有历史缓存，没有文件更改历史，`git HEAD^` 掉不回头。


如果是git 命令合并分支好说，可是用git 命令合并文件（课堂没有提到），初以为 `git merge-file`可以 

可是
> git-merge-file - Run a **three-way file** merge. //第三方啊

> git merge-file incorporates all changes that lead from the `<base-file> `to `<other-file> `into` <current-file>`. The result ordinarily goes into` <current-file>`. git merge-file is useful for combining separate changes to an original. Suppose` <base-file>` is the original, and both `<current-file> `and` <other-file>` are modifications of `<base-file>`, then git merge-file combines both changes.

4个文件又都是本地同一个文件夹的, 且没有历史缓存。

>git merge-file README.my README README.upstream
combines the changes of README.my and README.upstream since README, tries to merge them and writes the result into README.my.
//把从原初文件`READEME` 增减过的 `REAME.upstream` 里的内容写入 `REASME.my` 

难道是这样吗? 
试试吧，不过还是不同情况，走不通。。。
出现错误提醒 `Cannot merge binary files` //我又不懂操作了

*PS 1 : 我倒是希望能在`git`命令合并 .doc 的文件。。。莫非。。。不死心，于是第二个方向上尝试。。。*
*PS 2 :不至于在一开始作业就挖这个坑吧——可以弃坑了*


