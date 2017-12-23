# git
## General
git cherry-pick <commit_id>...  : pick the commit from other branch to current branch

### 假设要合并最后的2个提交，可以按如下命令进行：
```
git rebase –i HEAD~2
git merge --squash <branch> 把<branch>上所有的commit压缩，缺省是不commit
git push --delete origin <branch>
git checkout -b serverfix origin/serverfix
```
From <http://www.cnblogs.com/wujianlundao/archive/2012/07/30/2615873.html> 

### GIT查看、删除、重命名远程分支和TAG

  http://zengrong.net/post/1746.htm  

### 查看远程分支 
加上-a参数可以查看远程分支，远程分支会用红色表示出来（如果你开了颜色支持的话）：

在Git v1.7.0 之后，可以使用这种语法删除远程分支：

    git push origin --delete <branchName>

删除tag这么用：

    git push origin --delete tag <tagname>

否则，可以使用这种语法，推送一个空分支到远程分支，其实就相当于删除远程分支：

    git push origin :<branchName>

这是删除tag的方法，推送一个空tag到远程tag：
```
git tag -d <tagname>
git push origin :refs/tags/<tagname>
```
两种语法作用完全相同

### 删除不存在对应远程分支的本地分支
假设这样一种情况：
1. 我创建了本地分支b1并pull到远程分支 origin/b1；
2. 其他人在本地使用fetch或pull创建了本地的b1分支；
3. 我删除了 origin/b1 远程分支；
4. 其他人再次执行fetch或者pull并不会删除这个他们本地的 b1 分支，运行 git branch -a 也不能看出这个branch被删除了，如何处理？
使用下面的代码查看b1的状态：

```
# git remote show origin
* remote origin
  Fetch URL: git@github.com:xxx/xxx.git
  Push  URL: git@github.com:xxx/xxx.git
  HEAD branch: master
  Remote branches:
    master                 tracked
    refs/remotes/origin/b1 stale (use 'git remote prune' to remove)
  Local branch configured for 'git pull':
      master merges with remote master
    Local ref configured for 'git push':
      master pushes to master (up to date)
```
这时候能够看到b1是stale的，使用 git remote prune origin 可以将其从本地版本库中去除。更简单的方法是使用这个命令，它在fetch之后删除掉没有与远程分支对应的本地分支：

    git fetch -p

### 重命名远程分支
在git中重命名远程分支，其实就是先删除远程分支，然后重命名本地分支，再重新提交一个远程分支。例如下面的例子中，我需要把 devel 分支重命名为 develop 分支：
```
# git branch -av
* devel                             752bb84 Merge pull request #158 from Gwill/devel
  master                            53b27b8 Merge pull request #138 from tdlrobin/master
  zrong                             2ae98d8 modify CCFileUtils, export getFileData
  remotes/origin/HEAD               -> origin/master
  remotes/origin/add_build_script   d4a8c4f Merge branch 'master' into add_build_script
  remotes/origin/devel              752bb84 Merge pull request #158 from Gwill/devel
  remotes/origin/devel_qt51         62208f1 update .gitignore
  remotes/origin/master             53b27b8 Merge pull request #138 from tdlrobin/master
  remotes/origin/zrong              2ae98d8 modify CCFileUtils, export getFileData
```

### 删除远程分支：
```
# git push --delete origin devel
To git@github.com:zrong/quick-cocos2d-x.git
- [deleted]         devel
```

### 重命名本地分支：
   # git br -m devel develop

### 推送本地分支：
```
# git push origin develop
Counting objects: 92, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (48/48), done.
Writing objects: 100% (58/58), 1.38 MiB, done.
Total 58 (delta 34), reused 12 (delta 5)
To git@github.com:zrong/quick-cocos2d-x.git
* [new branch]      develop -> develop
```
然而，在 github 上操作的时候，我在删除远程分支时碰到这个错误：
```
# git push --delete origin devel
remote: error: refusing to delete the current branch: refs/heads/devel
To git@github.com:zrong/quick-cocos2d-x.git
! [remote rejected] devel (deletion of the current branch prohibited)
error: failed to push some refs to 'git@github.com:zrong/quick-cocos2d-x.git'
```

这是由于在 github 中，devel 是项目的默认分支。要解决此问题，这样操作：
1. 进入 github 中该项目的 Settings 页面；
2. 设置 Default Branch 为其他的分支（例如 master）；
3. 重新执行删除远程分支命令。

### 把本地tag推送到远程
    $ git push --tags

### 获取远程tag
    $ git fetch origin tag <tagname>

### 查看所有被Git忽略的文件
```
Git 1.6+:
git ls-files --others -i --exclude-standard
#Git 1.4, 1.5:
git ls-files --others -i \
--exclude-from="`git rev-parse --git-dir`/info/exclude" \
--exclude-per-directory=.gitignore
```
### 清除所有被Git忽略的文件或文件夹(小心)
查看在清理之前会做的操作

    git clean -Xn

清除文件或文件夹， -f 选项强制删除，-d删除目录（小心）

    git clean -Xdf

## 个性化你的Git Log的输出格式

git已经变成了很多程序员日常工具之一。

git log是查看git历史的好工具，不过默认的格式并不是特别的直观。

很多时候想要更简便的输出更多或者更少的信息，这里列出几个git log的format。

可以根据自己的需要定制。

git log命令可一接受一个--pretty选项，来确定输出的格式.

如果我们只想输出hash.
```
git log --pretty=format:"%h"
```
git用各种placeholder来决定各种显示内容： 
下面内容来自这里
```
- %H: commit hash
- %h: 缩短的commit hash
- %T: tree hash
- %t: 缩短的 tree hash
- %P: parent hashes
- %p: 缩短的 parent hashes
- %an: 作者名字
- %aN: mailmap的作者名字 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
- %ae: 作者邮箱
- %aE: 作者邮箱 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
- %ad: 日期 (--date= 制定的格式)
- %aD: 日期, RFC2822格式
- %ar: 日期, 相对格式(1 day ago)
- %at: 日期, UNIX timestamp
- %ai: 日期, ISO 8601 格式
- %cn: 提交者名字
- %cN: 提交者名字 (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
- %ce: 提交者 email
- %cE: 提交者 email (.mailmap对应，详情参照git-shortlog(1)或者git-blame(1))
- %cd: 提交日期 (--date= 制定的格式)
- %cD: 提交日期, RFC2822格式
- %cr: 提交日期, 相对格式(1 day ago)
- %ct: 提交日期, UNIX timestamp
- %ci: 提交日期, ISO 8601 格式
- %d: ref名称
- %e: encoding
- %s: commit信息标题
- %f: sanitized subject line, suitable for a filename
- %b: commit信息内容
- %N: commit notes
- %gD: reflog selector, e.g., refs/stash@{1}
- %gd: shortened reflog selector, e.g., stash@{1}
- %gs: reflog subject
- %Cred: 切换到红色
- %Cgreen: 切换到绿色
- %Cblue: 切换到蓝色
- %Creset: 重设颜色
- %C(...): 制定颜色, as described in color.branch.* config option
- %m: left, right or boundary mark
- %n: 换行
- %%: a raw %
- %x00: print a byte from a hex code
- %w([[,[,]]]): switch line wrapping, like the -w option of git-shortlog(1).
```
除此之外， --graph选项可以显示branch的ascii图例。

如果你自己定制了一个喜欢的输出方案，可以保存到git config，或者设置alias以便日后使用。

```
~/.gitconfig中加入:
[alias]
    lg = log --graph 
```

或者运行：

    git config --global alias.lg "log --graph"

最后来一个别人分享的例子，稍微有些慢，但是可以看下git log定制效果，效果很酷。。

    git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr)%Creset' --abbrev-commit --date=relative


