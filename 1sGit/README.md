# Git & GitHub
~ 上手、使用的心得体会

.git 

`git commit -am "xxx"` -am _add + commit 

`git diff` 会返回本地仓库和远程仓库的文件的不同。比如默认使用vim 打开 文本文件。

`git merge-file `
>A conflict occurs if both <current-file> and <other-file> have changes in a common segment of lines. If a conflict is found, git merge-file normally outputs a warning and brackets the conflict with lines containing <<<<<<<and>>>>>>> markers. A typical conflict will look like this:

```
<<<<<<< A
lines in file A
=======
lines in file B
>>>>>>> B
>>>>>>> 
```



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

解决办法还是有，
>[比较二进制文件](http://wiki.jikexueyuan.com/project/pro-git/customizing-git.html)

>你可以使用 Git 属性来有效地比较两个二进制文件（binary files，译注：指非文本文件）。那么第一步要做的是，告诉 Git 怎么把你的二进制文件转化为纯文本格式，从而让普通的 diff 命令可以进行文本对比。但是，我们怎么把二进制文件转化为文本呢？最好的解决方法是找到一个转换工具帮助我们进行转化。但是，大部分的二进制文件不能表示为可读的文本，例如语音文件就很难转化为文本文件。如果你遇到这些情况，比较简单的解决方法是从这些二进制文件中获取元数据。虽然这些元数据并不能完全描述一个二进制文件，但大多数情况下，都是能够概括文件情况的。

>下面，我们将会展示，如何使用转化工具进行二进制文件的比较。

>边注：有一些二进制文件虽然包含文字，但是却难以转换。（译注：例如 Word 文档。）在这些情况，你可以尝试使用 strings 工具来获取其中的文字。但如果当这些文档包含 UTF-16 编码，或者其他代码页（codepages），strings 也可能无补于事。strings 在大部分的 Mac 和 Linux 下都有安装。当遇到有二进制文件需要转换的时候，你可以试试这个工具。

**Word 文档**
>这个特性很酷，而且鲜为人知，因此我会结合实例来讲解。首先，要解决的是最令人头疼的问题：对 Word 文档进行版本控制。很多人对 Word 文档又恨又爱，如果想对其进行版本控制，你可以把文件加入到 Git 库中，每次修改后提交即可。但这样做没有一点实际意义，因为运行`git diff`命令后，你只能得到如下的结果：

>```
$ git diff
diff --git a/chapter1.doc b/chapter1.doc
index 88839c4..4afcb7c 100644
Binary files a/chapter1.doc and b/chapter1.doc differ
```

>你不能直接比较两个不同版本的 Word 文件，除非进行手动扫描，不是吗？ Git 属性能很好地解决此问题，把下面的行加到`.gitattributes`文件：

>```
*.doc diff=word
```


>当你要看比较结果时，如果文件扩展名是 "doc"，Git 调用 "word" 过滤器。什么是 "word" 过滤器呢？其实就是 Git 使用`strings` 程序，把 Word 文档转换成可读的文本文件，之后再进行比较：

>```
$ git config diff.word.textconv catdoc
```
>这个命令会在你的 `.git/config `文件中增加一节：

>```
[diff "word"]
    textconv = catdoc
```

>现在如果在两个快照之间比较以`.doc`结尾的文件，Git 对这些文件运用 "word" 过滤器，在比较前把 Word 文件转换成文本文件。

>下面展示了一个实例，我把此书的第一章纳入 Git 管理，在一个段落中加入了一些文本后保存，之后运行git diff命令，得到结果如下：

>```
$ git diff
diff --git a/chapter1.doc b/chapter1.doc
index c1c8a0a..b93c9e4 100644
--- a/chapter1.doc
+++ b/chapter1.doc
@@ -128,7 +128,7 @@ and data size)
 Since its birth in 2005, Git has evolved and matured to be easy to use
 and yet retain these initial qualities. It’s incredibly fast, it’s
 very efficient with large projects, and it has an incredible branching
-system for non-linear development.
+system for non-linear development (See Chapter 3).
```

>Git 成功且简洁地显示出我增加的文本 "(See Chapter 3)"。工作的很完美！


*PS 1 : 我倒是希望能在`git`命令合并 .doc 的文件。。。莫非。。。不死心，于是第二个方向上尝试。。。于是找到了上门的法子*
不管作业愿意所谓的“合并”了。


