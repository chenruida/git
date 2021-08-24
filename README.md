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
    - ![image-20210824103901208](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/image-20210824103901208bhX1E6.png)

- git reflog 查看每一次操作记录

## 工作区和暂存区

- 工作区 电脑里看到的目录

- 版本库 .git文件目录

- 添加进版本库工作流程

  1. ```git add``` 把文件添加进去，实际上就是把文件修改添加到暂存区；

  ![git-stage](https://www.liaoxuefeng.com/files/attachments/919020074026336/0)

  2. ```git commit ```提交更改，实际上就是把暂存区的所有内容提交到当前分支。

  ![git-stage-after-commit](https://www.liaoxuefeng.com/files/attachments/919020100829536/0)

## 撤销修改

- ```git checkout -- file``` 丢弃工作区的修改
  - 自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
  - 已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
  - `git checkout -- file`命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令
- ```git reset ```把暂存区的修改回退到工作区

## 删除文件

- `git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失**最近一次提交后你修改的内容**。

