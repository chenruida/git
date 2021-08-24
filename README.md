# 学习git

## 查看状态

- git status 掌握仓库当前的状态

![image-20210824103455395](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/image-2021082410345539565VMKz.png)

- git diff 查看difference

![image-20210824103531284](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/image-20210824103531284NU0MNp.png)

## 版本回退

- git log 查看历史记录

![image-20210824103642709](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/image-202108241036427092KCytl.png)

- git reset --head (commit id)
  - --hard 指向版本的指针
    - ![image-20210824103901208](https://cdn.jsdelivr.net/gh/chenruida/image@master/uPic/image-20210824103901208bhX1E6.png)

- git reflog 查看每一次操作记录

## 工作区和暂存区

- 工作区 电脑里看到的目录

- 版本库 .git文件目录

- 添加进版本库工作流程

  1. git add 把文件添加进去，实际上就是把文件修改添加到暂存区；

  ![git-stage](https://www.liaoxuefeng.com/files/attachments/919020074026336/0)

  2. git commit 提交更改，实际上就是把暂存区的所有内容提交到当前分支。

  ![git-stage-after-commit](https://www.liaoxuefeng.com/files/attachments/919020100829536/0)

  
