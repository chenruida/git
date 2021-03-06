# 学习git

## 查看状态

- ```git status ```掌握仓库当前的状态

![image-20210824103455395](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/image-2021082410345539565VMKz.png)

- ```git diff ```查看difference

![image-20210824103531284](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/image-20210824103531284NU0MNp.png)

## 版本回退

- ```git log``` 查看历史记录

![image-20210824103642709](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/image-202108241036427092KCytl.png)

- ```git reset --head (commit id)```
  - --hard 指向版本的指针
    - ![image-20210824103901208](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/image-20210824103901208bhX1E6CZi89h.png)

- git reflog 查看每一次操作记录

## 工作区和暂存区

- 工作区 电脑里看到的目录

- 版本库 .git文件目录

- 添加进版本库工作流程

  1. ```git add``` 把文件添加进去，实际上就是把文件修改添加到暂存区；

  ![git-stage](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/0-20210824110926630oIxDTA.jpeg)

  2. ```git commit ```提交更改，实际上就是把暂存区的所有内容提交到当前分支。

  ![git-stage-after-commit](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/0RAeORi.jpeg)

## 撤销修改

- ```git checkout -- file``` 丢弃工作区的修改
  
  - 自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
  - 已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
  - `git checkout -- file`命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令
  
- ```git reset ```把暂存区的修改回退到工作区

  - --mixed  
    - 意思是：不删除工作空间改动代码，撤销commit，并且撤销git add . 操作
    - 这个为默认参数,git reset --mixed HEAD^ 和 git reset HEAD^ 效果是一样的。

  - --soft  
    - 不删除工作空间改动代码，撤销commit，不撤销git add . 

  - --hard 
    - 删除工作空间改动代码，撤销commit，撤销git add . 
    - 注意完成这个操作后，就恢复到了上一次的commit状态。

## 删除文件

- `git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失**最近一次提交后你修改的内容**。

## 远程版本库

- `git remote -v`查看远程库信息
- `git remote rm <name>`命令删除远程库

## 分支管理

- 每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支
- 在Git里，这个分支叫主分支，即`master`分支。`HEAD`严格来说不是指向提交，而是指向`master`，`master`才是指向提交的，所以，`HEAD`指向的就是当前分支。

## 图解分支

一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点：

![git-br-initial](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/0-20210824110920893sQNjYi.png)

每次提交，`master`分支都会向前移动一步，这样，随着你不断提交，`master`分支的线也越来越长。

当我们创建新的分支，例如`dev`时，Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上：

![git-br-create](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/l-20210824110918805BTCcUe.png)

你看，Git创建一个分支很快，因为除了增加一个`dev`指针，改改`HEAD`的指向，工作区的文件都没有任何变化！

不过，从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变：

![git-br-dev-fd](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/l207sRE.png)

假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。Git怎么合并呢？最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并：

![git-br-ff-merge](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/0-20210824110914289ijejz7.png)

所以Git合并分支也很快！就改改指针，工作区内容也不变！

合并完分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉，删掉后，我们就剩下了一条`master`分支：

![git-br-rm](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/0yF0U5B.png)

## 创建和合并分支

- 查看分支：`git branch`
- 创建分支：`git branch <name>`
- 切换分支：`git checkout <name>`或者`git switch <name>`
- 创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`
- 合并某分支到当前分支：`git merge <name>`
- 删除分支：`git branch -d <name>`

## 合并冲突

- 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
- 解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
- 用`git log --graph`命令可以看到分支合并图。

## 分支策略

在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

所以，团队合作的分支看起来就像这样：

![git-br-policy](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/0-202108241126416464ijzuM.png)

合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

## bug分支

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；

在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支，避免重复劳动。

## 远程操作

- 查看远程库信息，使用`git remote -v`；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

## 变基

- rebase操作可以把本地未push的分叉提交历史整理成直线；
- rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

## 标签

- 命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
- 命令`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
- 命令`git tag`可以查看所有标签。
- 命令`git push origin <tagname>`可以推送一个本地标签；
- 命令`git push origin --tags`可以推送全部未推送过的本地标签；
- 命令`git tag -d <tagname>`可以删除一个本地标签；
- 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。

