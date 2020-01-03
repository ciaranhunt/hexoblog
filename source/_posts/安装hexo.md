---

title: 安装hexo
date: 2019-12-31 18:10:24
categories:
    -技术向
tags:
    -hexo

---

## 前言

我是参考[简书](https://www.jianshu.com/p/d49e4684e62b)这位老哥的教程的，算是很详细的了，主要是刚用 **deepin**（linux）不太熟悉，所以这位老哥对于我这种小白已经够详细了。中间有一个Github Page配置没有写，所以比较模糊。这也是我第一次使用博客，就以这个作为起点。这是我的[博客地址](https://ciaranhunt.github.io)。

<!--more-->

## 环境搭建

Hexo的介绍及详细信息请查看[官方文档](https://hexo.io/zh-cn/docs/index.html),以下是个人安装过程。

### 安装Git

```bash
sudo apt install git
```

安装完记得配置一下：

```bash
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

### 安装[Node.js](https://nodejs.org/en/)

我是直接通过官下载并解压的，没有通过命令行（新手还是不太会）. 
![lUm9hR.png](https://s2.ax1x.com/2020/01/03/lUm9hR.png)
将下载的压缩文件移动到/opt目录下解压，接下来配置环境变量，利用管理员权限打开 **/etc/profile** 文件，增添以下内容，注意等号后面没有空格，保存退出。为了使该环境变量生效，可以在终端执行 **source /etc/profile**，或者重启。

    # Node.js
    export NODE_HOME=/opt/node-v13.5.0linux-x64/bin
    export PATH=$PATH:$NODE_HOME
Node自带npm，但是npm更新频繁，要保持使最新版本，可以执行以下命令：

```bash
npm install npm -g
```

### 安装Hexo

```bash
npm install -g hexo-cli
```

如果碰到权限问题，可以参考：[处理npm权限问题](https://www.kancloud.cn/shellway/npm-doc/199985)
安装后查看是否安装成功，利用

```bash
hexo version
```

## 建站及配置

### 建站初始化

选择在 Documents 目录下创建 blog 文件夹来存放源文件。

```bash
cd ~/Documents
hexo init blog
cd blog
npm install
```

### 生成文件及本地调试

初始化后执行 **hexo generate**或 **hexo g**可生成静态文件（public 文件夹）与缓存文件（data.json）。然后我们执行 **hexo server** 或 **hexo s** 就可以启动本地服务器，访问网址 http://localhost:4000/ 就可以查看文章效果了。
![lUmdCn.png](https://s2.ax1x.com/2020/01/03/lUmdCn.png)

### 部署到Github Page

1.我已经有了Github的账号，先新建一个项目，名字必须为**username.github.io**。
    
    注意：名字必须为username.github.io。
2.进入项目的setting进行配置Github Page。
![lUnpqS.png](https://s2.ax1x.com/2020/01/03/lUnpqS.png)
3.安装相关插件

    注意：插件下载时需要在博客的文件夹中，在本文就是 blog 文件夹！

```bash
cd ~/Documents/blog
npm install hexo-deployer-git --save
```

4.然后修改Hexo的配置文件，位于blog文件夹下的**_comfig.yml**的最后几行

    # Deployment
    ## Docs: https://hexo.io/docs/deployment.html
    deploy:
        type: git
    repo:
        git@github.com:ciaranhunt/ciaranhunt.github.io.git
    branch: master
5.要发的博客内容位于blog/source/_posts，新建md文件即可，每次命令行切换到blog目录下，

```bash
hexo g
hexo d
```

6.创作时Front-Matter
![lUnnqU.png](https://s2.ax1x.com/2020/01/03/lUnnqU.png)
7.还可以修改一下URL，绑定创建的Github Page

    url: https://ciaranhunt.github.io

## Hexo配置件简析

上文提到了 _config.yml 这一配置文件，它是关于网站的一些配置，具体说明可见 Hexo 官方文档。以下对官网有详细说明的内容就不再赘述，优先查看官网文档也是个好习惯。


    # Site 网站
    # URL 网址
    # Directory 目录
    # Writing 文章
    # Home page setting 主页相关设置
    # Category & Tag 分类 & 标签
    # Date / Time format 日期 / 时间格式
    # Pagination 分页
    # Extensions 插件
以上内容在官网中都有详细的说明介绍，在你搭建的开始，不需要在配置上面花费过多的精力，大部分保持默认设置即可。这里只补充说明有必要修改的部分。

### Site 网站

这一部分是显示在页面上的重要基本信息，如网站的标题、作者、说明等。这一定是要修改的，以我的配置为例：

    # Site
    title: ciaranhunt # 博客标题
    subtitle: Don't Repeat Yourself # 博客副标题
    description:  君子坦荡荡 小人长戚戚 # 博客描述，部分主题会用来生成简介
    keywords: # 通常建议包含网站的关键词
    author: ciaranhunt # 博客作者，部分主题会用来显示作者
    language: zh-CN # 语言，具体需要查看主题theme说明
    timezone: # 默认使用电脑的时区

### URL 网址

只需要修改上一步提到的就行，其他默认即可.

### Home page setting 主页相关设置

默认配置文件中只写了 index_generator 这部分，也就是首页的配置，事实上，查看 node_modules 文件中，可以看到有以下几个 generator：

    ├── hexo-generator-archive
    ├── hexo-generator-category
    ├── hexo-generator-index
    ├── hexo-generator-tag
这也表明了我们博客可以通过以上几个维度来展示你的文章，它们分别是归档、分类、索引、标签，其中对于分类与标签我个人理解是一篇文章最好使用一个类别(category)和多个标签(tag)。

## 主题

### 安装主题

以Next主题为例

```bash
cd blog
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

### 更新主题

```bash
cd blog/themes/next
git pull --rebase
```

### 切换主题

在 Hexo 中切换主题需要修改站点配置文件中的 theme 一节。

从预览可以看到，虽然站点配置文件设置了网站的语言为 zh-Hans 但还是英语显示（我是说主页与归档这两个词……），原因其实很简单，NexT 主题中，中文需要指定的 language 字段不是 zh-Hans，而是 zh-CN，所以 language 字段的配置需要查看具体的主题是如何定义。NexT 的语言列表对应关系可见 NexT 主题语言文件夹：themes/next/language/，修改之后再次预览就可以看到切换为中文显示了。

修改了站点配置文件已经可以使用上简洁的 NexT 主题了，而主题还可以进行配置使得显示效果更符合你的心意。

## 主题配置文件

### 外观（Scheme）

NexT 主题通过 Scheme 设置可展现出不同的外观。而且几乎可以说所有的配置都可以在 Scheme 之间共用。
修改主题配置文件 scheme 一节：

    # Schemes
    #scheme: Muse
    #scheme: Mist
    #scheme: Pisces
    scheme: Gemini
当前提供了四种样式，去掉某一样式的行首注释即可使用，修改之后可预览查看显示效果。你可以修改选择自己喜欢的样式。

### 菜单（Menu）

在修改站点配置文件的时候说到博客可以显示归档、分类、标签等，下面展示如何修改主题配置文件使得能够真正地展示这几个页面。

修改主题配置文件 menu 一节：

    menu:
      home: / || home
      #about: /about/ || user
      tags: /tags/ || tags # 取消注释，需要手动创建该页面
      categories: /categories/ || th # 取消注释，需要手动创建该页面
      archives: /archives/ || archive
      #schedule: /schedule/ || calendar
      #sitemap: /sitemap.xml || sitemap
      #commonweal: /404/ || heartbeat
取消 tags 和 categories 两行的注释，预览可以看到已经在界面上显示这两个菜单了，但单击选择时页面提示：Cannot GET /categories/ ，这是因为我们还未创建对应的页面。

## 完成基础搭建

经过以上步骤，一个 Hexo 博客已经搭建出来了，并且我们可以愉快地发表文章了！

后续可修改的内容还有很多，可以给博客添加更多的功能如搜索、评论、阅读量统计等，还可以对博客进行个性化定制如头像、背景的修改等等。这些内容我们可以查看主题的说明文档、网站、配置文件，它们一般都对支持的配置进行了说明。

博客的修改暂且不表，后续还要考虑一个问题：程序员一般都不只一台电脑，想在不同电脑上都能维护博客怎么办？或者说以上配置、发布的内容丢失了，博客又怎么找回？可以看到，远程仓库中上传的只有编译好的网页文件，而没有这些博客源文件、文章、主题、配置等，因此我们需要合理备份这些内容来解决上面这个问题。