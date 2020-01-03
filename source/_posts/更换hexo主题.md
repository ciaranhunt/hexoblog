---
title: 更换hexo主题
date: 2019-12-31T18:10:24.000Z
categories: '-技术向'
tags: '-hex'
---

## 前言

刚安装hexo的时候就已经安装了Next主题，之后又想安装其它主题，找到了[suka主题](https://theme-suka.skk.moe/),本来打算不折腾，没想到又折腾到manjaro了（不过manjaro的自定义程度是真的高）。好了，开始！

<!-- more -->
## 下载suka

### 1.可以直接在官方的github的Realese页面下载

- [下载最新Realese版本](https://github.com/SukkaW/hexo-theme-suka/releases/latest)

      最新的释出版本，适合绝大部分用户

- [下载 Canary 版本](https://github.com/SukkaW/hexo-theme-suka/archive/canary.zip)

      包含最新的、尚在开发中的特性，可能不稳定；适合进阶用户和开发者。

- [下载 其它 版本](https://github.com/SukkaW/hexo-theme-suka/releases)

        你可以自己决定想要使用的版本；部分版本可能不再提供技术支持。

    ![lUlMCQ.png](https://s2.ax1x.com/2020/01/03/lUlMCQ.png)

### 2.你可以自己决定想要使用的分支；使用 Git 下载「Suka」以后还可以使用 git pull 更新「Suka」

```bash
cd themes
git clone https://github.com/SukkaW/hexo-theme-suka.git suka
cd suka
git checkout {branch/tags name/commit hash}
```

## 安装suka

和其他主题不同，安装「Suka」需要额外的步骤；前往「Suka」主题目录下执行 npm install --production 指令安装「Suka」运行时所必须的依赖。

```bash
cd themes/suka
npm install --production
```

同时你需要把「Suka」主题目录下的 _config.example.yml 复制一份并把副本重命名为 _config.yml。

```shell
cp -i _config.example.yml _config.yml
```

然后回到站点根目录，执行：  

`bash cat /themes/suka/site_config.yml >> _config.yml`  
现在你的 **站点配置文件** 应该是这样:
![lUltET.png](https://s2.ax1x.com/2020/01/03/lUltET.png)

## 运行suka

```bash
hexo g
hexo d
```

## 更新suka

如果你是在 版本发布页 下载并安装的「Suka」，那么你需要备份你的 主题备份文件，然后将旧的主题文件夹命名为 **suka-old**，将下载的新版本「Suka」重命名为 **suka**，根据更新日志的指导迁移旧的 主题配置文件 到新的 主题配置文件 中。测试通过后你可以将 **suka-old** 删除。

如果你使用 **Git** 安装的「Suka」，你可以直接在主题文件夹下运行 **git pull** 更新主题，并把备份之前的 主题配置文件 重命名为 **_config.old.yml**，复制一份**_config.example.yml** 并重命名为 **_config.yml**。从 **_config.old.yml** 迁移你的配置到新的 **_config.yml**测试通过后你可以将 **_config.old.yml** 删除。

        注意:一定要备份一下

## Butterfly主题

### 平滑升级

为了主题的平滑升级, Butterfly使用了data files特性。

推荐把主题默认的配置文件_config.yml复制到Hexo工作目录下的source/_data/butterfly.yml，如果source/_data的目录不存在那就创建一个。

    注意，如果你创建了butterfly.yml,它将会替换主题默认配置文件_config.yml里的配置项( 不是合并而是替换 ),之后你就只需要通过git pull的方式就可以平滑地升级theme-butterfly了。

### Page Front-matter

    --- 
        title: 
        date: 
        tags: 
        categories: 
        keywords: 
        description: 
        top_img: （除非特定需要，可以不写）
        comments是否显示评论（除非设置false,可以不写）
        cover:缩略图
        toc:是否显示toc （除非特定文章设置，可以不写）
        toc_number:是否显示toc数字（除非特定文章设置，可以不写）
        copyright:是否显示版权（除非特定文章设置，可以不写）
        mathjax: 
        katex: 
        hide: 
    ---

