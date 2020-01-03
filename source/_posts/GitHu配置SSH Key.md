---
title: GitHub如何配置SSH Key
date: 2020-01-02 15:21:51
categories:
    -技术向
tags:
    -Github
---
    https://github.com/ciaranhunt/ciaranhunt.github.io.git
    git@github.com:ciaranhunt/ciaranhunt.github.io.git
这两个地址展示的是同一个项目，但是这两个地址之间有什么联系呢？
前者是**https url**直接有效网址打开，但是用户每次通过git提交的时候都要输入用户名和密码，有没有简单的一点的办法，一次配置，永久使用呢？当然，所以有了第二种地址，也就是**SSH URL**，那如何配置就是本文要分享的内容。
GitHub配置SSH Key的目的是为了帮助我们在通过git提交代码是，不需要繁琐的验证过程，简化操作流程。
<!--more-->

## 设置git的user name和email

如果你是第一次使用，或者还没有配置过的话需要操作一下命令，自行替换相应字段。

```bash
git config --global user.name "yourname"
git config --global user.email  "your@example.com"
```

说明：git config --list 查看当前Git环境所有配置，还可以配置一些命令别名之类的.

## 检查是否存在SSH Key

```bash
cd ~/.ssh
ls
或者
ll
```

看是否存在 id_rsa 和 id_rsa.pub文件，如果存在，说明已经有SSH Key
![lUlBvR.png](https://s2.ax1x.com/2020/01/03/lUlBvR.png)
如果没有SSH Key，则需要先生成一下

```bash
ssh-keygen -t rsa -C "571074750@qq.com"
```

## 获取SSH Key

```bash
cat id_rsa.pub
```

![lUlyb6.png](https://s2.ax1x.com/2020/01/03/lUlyb6.png)

## GitHub添加SSH Key

1. GitHub点击用户头像，选择setting
2. 选择SSH and GPGkeys
3. 新建一个SSH Key  

取个名字，把之前拷贝的秘钥复制进去，添加就好啦。

## 验证

测试是否成功配置SSH Key

```bash
ssh -T git@github.com
//运行结果出现类似如下
Hi xiangshuo1992! You've successfully authenticated, but GitHub does not provide shell access.
```