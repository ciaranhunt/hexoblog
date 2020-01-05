---
title: github相关指令
date: 2020-01-04 21:31:28
categories:
    -技术向
tags:
    -Github
top_img: https://s2.ax1x.com/2020/01/04/lwqRj1.md.jpg
cover: https://s2.ax1x.com/2020/01/04/lwqsNF.png
---
## 基本操作

### 第一次提交远程仓库

切换到要提交的文件根目录

```bash
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/ciaranhunt/test3.git
git push -u origin master
```

#### 更新被拒绝，因为您当前分支的最新提交落后于其对应的远程分支

解决方案：需要先获取远端更新并与本地合并,再git push

```bash
git remote add origin https://github.com/miaoihan/weibo.git
git fetch origin //获取远程更新
git merge origin/master //把更新的内容合并到本地分支
```

上面的名字，和*.git改成自己的
