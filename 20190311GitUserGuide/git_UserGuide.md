# git使用手册



##20190311 Terminal上传文件

cd ~/Desktop PicturesWY

cd 20190311JupyterNotebook

git add JupyterNotebook_SetUp_macOS.md

git commit JupyterNotebook_SetUp_macOS.md -m "add file for set up Jupyter Notebook macOS"

git branch -a

git push origin master



但是这样是新上传了一个folder 而不是重命名folder+更新内容



## 20190311Terminal push更新整包内容

cd ~/Desktop

cd PicturesWY

```
wangyudeMacBook-Pro:PicturesWY wangyu$ git add 20190311JupyterNotebook
wangyudeMacBook-Pro:PicturesWY wangyu$ git commit 20190311JupyterNotebook -m "add file for macOS"
[master 9d9f4a7] add file for macOS
 Committer: Yu Wang <wangyu@wangyudeMacBook-Pro.local>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

​```
git config --global --edit
​```

After doing this, you may fix the identity used for this commit with:

​```
git commit --amend --reset-author
​```

 13 files changed, 11 insertions(+)
 create mode 100644 20190311JupyterNotebook/20190311.md
 create mode 100644 20190311JupyterNotebook/Screen Shot 2019-03-11 at 10.25.35 PM.png
 create mode 100644 20190311JupyterNotebook/Screen Shot 2019-03-11 at 10.27.00 PM.png
 create mode 100644 20190311JupyterNotebook/Screen Shot 2019-03-11 at 12.52.27 PM.png
 create mode 100644 20190311JupyterNotebook/Screen Shot 2019-03-11 at 12.56.33 PM.png
 create mode 100644 20190311JupyterNotebook/Screen Shot 2019-03-11 at 12.58.37 PM.png
 create mode 100644 20190311JupyterNotebook/Screen Shot 2019-03-11 at 12.59.20 PM.png
 create mode 100644 20190311JupyterNotebook/Screen Shot 2019-03-11 at 3.57.20 PM.png
 create mode 100644 20190311JupyterNotebook/Screen Shot 2019-03-11 at 5.02.42 PM.png
 create mode 100644 20190311JupyterNotebook/Screen Shot 2019-03-11 at 8.36.14 PM.png
 create mode 100644 20190311JupyterNotebook/Screen Shot 2019-03-11 at 8.43.07 PM.png
 create mode 100644 20190311JupyterNotebook/Screen Shot 2019-03-11 at 8.43.24 PM.png
 create mode 100644 20190311JupyterNotebook/Screen Shot 2019-03-11 at 9.52.32 PM.png
```



```
wangyudeMacBook-Pro:PicturesWY wangyu$ git branch -a

master
remotes/origin/HEAD -> origin/master
remotes/origin/master
```

```
wangyudeMacBook-Pro:PicturesWY wangyu$ git branch -v

master 9d9f4a7 [ahead 1] add file for macOS
```

```
wangyudeMacBook-Pro:PicturesWY wangyu$ git push origin master
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 831 bytes | 831.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/SallyWY/PicturesWY.git
 2463095..9d9f4a7  master -> master
wangyudeMacBook-Pro:PicturesWY wangyu$ ls
20190311JupyterNotebook	README.md
```

```
wangyudeMacBook-Pro:PicturesWY wangyu$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

new file:   .DS_Store
deleted:    20190311Miniconda3/20190311.md
deleted:    20190311Miniconda3/Screen Shot 2019-03-11 at 10.25.35 PM.png
deleted:    20190311Miniconda3/Screen Shot 2019-03-11 at 10.27.00 PM.png
deleted:    20190311Miniconda3/Screen Shot 2019-03-11 at 12.52.27 PM.png
deleted:    20190311Miniconda3/Screen Shot 2019-03-11 at 12.56.33 PM.png
deleted:    20190311Miniconda3/Screen Shot 2019-03-11 at 12.58.37 PM.png
deleted:    20190311Miniconda3/Screen Shot 2019-03-11 at 12.59.20 PM.png
deleted:    20190311Miniconda3/Screen Shot 2019-03-11 at 3.57.20 PM.png
deleted:    20190311Miniconda3/Screen Shot 2019-03-11 at 5.02.42 PM.png
deleted:    20190311Miniconda3/Screen Shot 2019-03-11 at 8.36.14 PM.png
deleted:    20190311Miniconda3/Screen Shot 2019-03-11 at 8.43.07 PM.png
deleted:    20190311Miniconda3/Screen Shot 2019-03-11 at 8.43.24 PM.png
deleted:    20190311Miniconda3/Screen Shot 2019-03-11 at 9.52.32 PM.png

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

modified:   .DS_Store
```



## 20190311 Terminal 版本回退	

repository搞乱了

先进入到github网页版中，在commit内找到所希望的版本

![](https://github.com/SallyWY/PicturesWY/raw/master/20190311GitUserGuide/Screen%20Shot%202019-03-12%20at%2012.24.32%20AM.png)

点击最右边的<>左边的号码，也就是 “9d9f4a7”

然后复制commit 后面的一长串数字/字母（commit id）

![](https://github.com/SallyWY/PicturesWY/raw/master/20190311GitUserGuide/Screen%20Shot%202019-03-12%20at%2012.26.27%20AM.png)

使用git push发现不可以

于是使用 git push —force强制更新

最终实现版本回退

```
wangyudeMacBook-Pro:PicturesWY wangyu$ ls
20190311JupyterNotebook	README.md
wangyudeMacBook-Pro:PicturesWY wangyu$ git reset --hard 9d9f4a7fd9314b36fba0ff16cf8946e13f793a13
HEAD is now at 9d9f4a7 add file for macOS
wangyudeMacBook-Pro:PicturesWY wangyu$ git reset 9d9f4a7fd9314b36fba0ff16cf8946e13f793a13
```

```
wangyudeMacBook-Pro:PicturesWY wangyu$ git branch -v
master 9d9f4a7 [behind 2] add file for macOS
wangyudeMacBook-Pro:PicturesWY wangyu$ git push
To https://github.com/SallyWY/PicturesWY.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/SallyWY/PicturesWY.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
wangyudeMacBook-Pro:PicturesWY wangyu$ git push --force
Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/SallyWY/PicturesWY.git
87f5568...9d9f4a7 master -> master (forced update)
```

git log 可以查看更新日志

```
wangyudeMacBook-Pro:PicturesWY wangyu$ git log
commit 9d9f4a7fd9314b36fba0ff16cf8946e13f793a13 (HEAD -> master, origin/master, origin/HEAD)
Author: Yu Wang <wangyu@wangyudeMacBook-Pro.local>
Date:   Mon Mar 11 23:54:50 2019 +0100

add file for macOS

commit 2463095f040000a192b6a460e95100f81c4e1768
Author: Yu Wang <wangyu@wangyudeMacBook-Pro.local>
Date:   Mon Mar 11 23:49:32 2019 +0100

add file for set up Jupyter Notebook macOS

commit 5ac5125fd6c1e111680126d8d9aa070bb2ad6ab0
Author: SallyWY <sallywangyu@163.com>
Date:   Mon Mar 11 22:35:22 2019 +0100

Add files via upload

commit ecebac38fe236ff7bce2edf9f28e02374f580234
Author: SallyWY <sallywangyu@163.com>
Date:   Mon Mar 11 22:27:18 2019 +0100

Add files via upload
```

这证明 每次commit的-m还是要写的 方便查看commit版本



## 20190311 流畅实现git push

```
wangyudeMacBook-Pro:Desktop wangyu$ cd PicturesWY
wangyudeMacBook-Pro:PicturesWY wangyu$ ls
20190311GitUserGuide	20190311Miniconda3
20190311JupyterNotebook	README.md

wangyudeMacBook-Pro:PicturesWY wangyu$ git add 20190311GitUserGuide
wangyudeMacBook-Pro:PicturesWY wangyu$ git commit 20190311GitUserGuide -m "Git User Guide"
[master 3857279] Git User Guide
 Committer: Yu Wang <wangyu@wangyudeMacBook-Pro.local>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 3 files changed, 200 insertions(+)
 create mode 100644 20190311GitUserGuide/Screen Shot 2019-03-12 at 12.24.32 AM.png
 create mode 100644 20190311GitUserGuide/Screen Shot 2019-03-12 at 12.26.27 AM.png
 create mode 100644 "20190311GitUserGuide/git\344\275\277\347\224\250\346\211\213\345\206\214.md"

wangyudeMacBook-Pro:PicturesWY wangyu$ git branch -v
* master 3857279 [ahead 1] Git User Guide
wangyudeMacBook-Pro:PicturesWY wangyu$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
wangyudeMacBook-Pro:PicturesWY wangyu$ git push origin master
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 152.61 KiB | 25.43 MiB/s, done.
Total 6 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/SallyWY/PicturesWY.git
   9d9f4a7..3857279  master -> master
```

