# git 常用指令

在git完成安装后应首先注册用户名user.name 与邮箱user.email：
$ git config user.name "zhuxj"
$ git config user.email "xazhuxj@qq.com"


## 1 git init 
作用：建立git版本库(repository)

在当前文件夹下会建一个文件夹 .git 作为git的版本库

此时可用 git status 命令查看:

## 2 git status
作用：查看状态

$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)


## 3 git add 

作用：将文件加入工作区

创建文件 readme.txt 与 git命令指南.md 两文件

用 git status 命令查看:

$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        "git\345\221\275\344\273\244\346\214\207\345\215\227.md"
        readme.txt

nothing added to commit but untracked files present (use "git add" to track)


以上说明：readme.txt 与 git命令指南.md 两文件处于Untracked files:状态


将文件加入工作区：
$ git add readme.txt
warning: LF will be replaced by CRLF in readme.txt.
The file will have its original line endings in your working directory.

$ git add git命令指南.md

再查看其状态: 
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   "git\345\221\275\344\273\244\346\214\207\345\215\227.md"
        new file:   readme.txt

## 4 git commit
作用：将工作区文件提交到版本库中

$ git commit -m "readme.txt and git-guide.md"
[master (root-commit) 8a3bb69] readme.txt and git-guide.md
 2 files changed, 26 insertions(+)
 create mode 100644 "git\345\221\275\344\273\244\346\214\207\345\215\227.md"
 create mode 100644 readme.txt

 git commit 命令后的 -m "****" 必须写

 ## 5 时光穿梭
 将readme.txt的第一行修改为Git is a distributed version control system.
（比原来多了一个distributed）

查看状态为：
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   "git\345\221\275\344\273\244\346\214\207\345\215\227.md"
        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")

查看readme.txt的修改情况：
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
