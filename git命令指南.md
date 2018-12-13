# git 常用指令

在git完成安装后应首先注册用户名user.name 与邮箱user.email：
```
$ git config user.name "zhuxj"
$ git config user.email "xazhuxj@qq.com"
```

## 1 git init 
作用：建立git版本库(repository)

在当前文件夹下会建一个文件夹 .git 作为git的版本库

此时可用 git status 命令查看:

## 2 git status
作用：查看状态

```
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

## 3 git add 

作用：将文件加入工作区

创建文件 readme.txt 与 git命令指南.md 两文件

用 git status 命令查看:
```
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        "git\345\221\275\344\273\244\346\214\207\345\215\227.md"
        readme.txt

nothing added to commit but untracked files present (use "git add" to track)
```

以上说明：readme.txt 与 git命令指南.md 两文件处于Untracked files:状态

将文件加入工作区：
```
$ git add readme.txt
warning: LF will be replaced by CRLF in readme.txt.
The file will have its original line endings in your working directory.

$ git add git命令指南.md
```
再查看其状态:
```
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   "git\345\221\275\344\273\244\346\214\207\345\215\227.md"
        new file:   readme.txt
```

## 4 git commit
作用：将工作区文件提交到版本库中
```
$ git commit -m "readme.txt and git-guide.md"
[master (root-commit) 8a3bb69] readme.txt and git-guide.md
 2 files changed, 26 insertions(+)
 create mode 100644 "git\345\221\275\344\273\244\346\214\207\345\215\227.md"
 create mode 100644 readme.txt
```
 git commit 命令后的 -m "****" 必须写

当一个git commit 命令执行之后，再git status，会显示：
```
`$ git status                                                              
On branch master                                                                
nothing to commit, working tree clean  
```

表明：工作目录是干净的（working tree clean）

 ## 5 时光穿梭

 ### 5.1 准备
 将readme.txt的第一行修改为Git is a distributed version control system.
（比原来多了一个distributed）

+ (1) 查看状态为：
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   "git\345\221\275\344\273\244\346\214\207\345\215\227.md"
        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
+ (2) 查看readme.txt的修改情况：
```
$ git diff readme.txt
warning: LF will be replaced by CRLF in readme.txt.
The file will have its original line endings in your working directory.
diff --git a/readme.txt b/readme.txt
index 46d49bf..9247db6 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
```
+ (3) 添加修改后的文件：
```
$ git add readme.txt
warning: LF will be replaced by CRLF in readme.txt.
The file will have its original line endings in your working directory.
```
+ (4) 再次提交
```
$ git add git命令指南.md

$ git commit -m  "add distributed"
[master e607fc3] add distributed
 2 files changed, 91 insertions(+), 7 deletions(-)
```
+ (5) 再次修改提交
  将readme.txt文件第2行修改为：
  Git is free software distributed under the GPL.
  再次git add 与 git commit -m "append GPL"

### 5.2 提交日志查看：git log

```
$ git log
commit 9e5e3b17bfc19e1e82eeee34569794ff151b5212 (HEAD -> master)
Author: zhuxj <xazhuxj@qq.com>
Date:   Thu Dec 13 16:31:42 2018 +0800

    append GPL

commit e607fc38e2fe8baef6a16c02deba4e77336249f9
Author: zhuxj <xazhuxj@qq.com>
Date:   Thu Dec 13 16:22:24 2018 +0800

    add distributed

commit 8a3bb697a3f2cd4ad0b43f97f7bdb5968a317a3e
Author: zhuxj <xazhuxj@qq.com>
Date:   Thu Dec 13 16:09:55 2018 +0800

    readme.txt and git-guide.md
```

或者 
```
$ git log --pretty=oneline
9e5e3b17bfc19e1e82eeee34569794ff151b5212 (HEAD -> master) append GPL
e607fc38e2fe8baef6a16c02deba4e77336249f9 add distributed
8a3bb697a3f2cd4ad0b43f97f7bdb5968a317a3e readme.txt and git-guide.

$ git log --pretty=oneline
ec59fbf5593e94451ed09a62a4bb96cdf30d2a76 (HEAD -> master) modified git-guide.md
9e5e3b17bfc19e1e82eeee34569794ff151b5212 append GPL
e607fc38e2fe8baef6a16c02deba4e77336249f9 add distributed
8a3bb697a3f2cd4ad0b43f97f7bdb5968a317a3e readme.txt and git-guide.md
```

在Git中，用:
  + HEAD表示当前版本，也就是最新的提交
  + 上一个版本就是HEAD^，
  + 上上一个版本就是HEAD^^，
  + 往上100个版本写100个^比较容易数不过来，所以写成HEAD~100

### 5.3 版本回退：git reset --hard HEAD^
```
$ git reset --hard HEAD^
HEAD is now at 9e5e3b1 append GPL

$ git reset --hard HEAD^
HEAD is now at e607fc3 add 

$ git reset --hard ec59f
HEAD is now at ec59fbf modified git-guide.md
```

### 5.4 命令历史：git reflog
```
$ git reflog
ec59fbf (HEAD -> master) HEAD@{0}: reset: moving to ec59f
e607fc3 HEAD@{1}: reset: moving to HEAD^
9e5e3b1 HEAD@{2}: reset: moving to HEAD^
ec59fbf (HEAD -> master) HEAD@{3}: commit: modified git-guide.md
9e5e3b1 HEAD@{4}: commit: append GPL
e607fc3 HEAD@{5}: commit: add distributed
8a3bb69 HEAD@{6}: commit (initial): readme.txt and git-guide.md
```

## 6 版本库（Repository）

### 6.1 工作区与暂存区

工作区有一个隐藏目录.git，它是Git的版本库。

![git工作区文件状态](.\git-files-status.png "git工作区文件状态")



其对应的命令显示状态为：

```
$ git status                                                                    
On branch master                                                                
Changes not staged for commit:                                                  
(use "git add ..." to update what will be committed)                    
(use "git checkout -- ..." to discard changes in working directory)     
modified:   "git\345\221\275\344\273\244\346\214\207\345\215\227.md"    
modified:   readme.txt                                                  
Untracked files:                                                                
(use "git add ..." to include in what will be committed)                
GPL.jpg                                                                 
LICENSE.txt                                                             
git-files-status.png                                                    
no changes added to commit (use "git add" and/or "git commit -a")   
```

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

![git工作区与版本库](.\git-repository.jpg "git工作区与版本库")

把文件往Git版本库里添加的时候，是分两步执行的：

第1步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区； 

第2步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。


```
$ git add .                                                                     
warning: LF will be replaced by CRLF in LICENSE.txt.                            
The file will have its original line endings in your working directory          
zhuxj@CHINA-20181009K MINGW64 /c/Users/zhuxj/Desktop/git-ex (master)            
$ git commit -m "add LICENSE.TXT and GPL.jpg"                                   
[master e673b26] add LICENSE.TXT and GPL.jpg                                    
5 files changed, 71 insertions(+), 22 deletions(-)                             
create mode 100644 GPL.jpg                                                     
create mode 100644 LICENSE.txt                                                 
create mode 100644 git-files-status.png 
```

git commit命令成功执行后的示意图：

![git-commit后示意图](.\git-commit.jpg "git-commit后示意图")



**暂存区(stage)**是Git非常重要的概念

### 6.2 管理修改

**Git跟踪并管理的是修改，而非文件**

将readme.txt中第3行中的multable改为mutable，添加 一行：

Git tracks changes.

则有：

+ 未做 ***git add .*** 命令前：

```
$ git status                                                                    
On branch master                                                                
Changes not staged for commit:                                                  
(use "git add ..." to update what will be committed)                    
(use "git checkout -- ..." to discard changes in working directory)     
modified:   "git\345\221\275\344\273\244\346\214\207\345\215\227.md"    
modified:   readme.txt                                                  
Untracked files:                                                                
(use "git add ..." to include in what will be committed)                
git-commit.jpg                                                          
no changes added to commit (use "git add" and/or "git commit -a")     
```
查看文件readme.txt的差异：
```
$ git diff readme.txt                                                           
diff --git a/readme.txt b/readme.txt                                            
index bffec1e..db28b2c 100644                                                   
--- a/readme.txt                                                                
+++ b/readme.txt                                                                
@@ -1,3 +1,4 @@                                                                 
Git is a distributed version control system.                                   
Git is free software distributed under the GPL.                                
-Git has a multable index called stage.                                         
\ No newline at end of file                                                     
+Git has a mutable index called stage.                                          
+Git tracks changes.                                                            
\ No newline at end of file 
```

执行 ***git add .*** 命令后：
```
$ git add .                                                             
$ git status                                                                    
On branch master                                                                
Changes to be committed:                                                        
(use "git reset HEAD ..." to unstage)                                   
new file:   git-commit.jpg                                              
modified:   "git\345\221\275\344\273\244\346\214\207\345\215\227.md"    
modified:   readme.txt                                                  ```
```

再次修改再修改readme.txt中最后一行为Git tracks changes of files.

查看：

```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   git-commit.jpg
        modified:   "git\345\221\275\344\273\244\346\214\207\345\215\227.md"
        modified:   readme.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.txt
```

然后提交：

```

```

再查看                                                    
```
$ git status 
On branch master                                                                
Changes not staged for commit:                                                  
(use "git add ..." to update what will be committed)                    
(use "git checkout -- ..." to discard changes in working directory)     
modified:   readme.txt                                                  
no changes added to commit (use "git add" and/or "git commit -a")        
```

则第二次修改的未进行提交。

说明：git commit 只提交stage中的修改。

用命令可以查看：

```

```

正确的执行应为：

第一次修改 -> `git add` -> 第二次修改 -> `git add` -> `git commit`

**每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中**



### 6.3  撤销修改

如果在readme.txt尾添加一句：My stupid boss still prefers SVN.

后边想删除它，则：

+ 未git add时（修改还没有 add 到暂存区）：

```
   $ git status                                                                    
  On branch master                                                                
  Changes not staged for commit:                                                  
  (use "git add ..." to update what will be committed)                    
  (use "git checkout -- ..." to discard changes in working directory)     
  modified:   readme.txt                                                  
  no changes added to commit (use "git add" and/or "git commit -a")     
```

则可以：

```
$ git checkout -- readme.txt

```

+ 已经git add时（修改已经 add 到暂存区）：

  ```
  $ git add .
  $ git status
  On branch master
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
  
          modified:   "git\345\221\275\344\273\244\346\214\207\345\215\227.md"
          modified:   readme.txt
  ```

  需用 命令`git reset HEAD <file>`把暂存区的修改撤销掉（unstage），

  再 git checkout -- readme.txt 可将最后添加的修改删除。 

```
$ git reset HEAD readme.txt
Unstaged changes after reset:
M       readme.txt

$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   "git\345\221\275\344\273\244\346\214\207\345\215\227.md"

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.txt
```



+ 场景1：

  当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

+ 场景2：

  当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。

+ 场景3：

  已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退，不过前提是没有推送到远程库。