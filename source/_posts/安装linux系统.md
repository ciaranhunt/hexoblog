---
title: 安装Linux系统
date: 2020-01-02 14:33:08
categories:
    -技术向
tags:
    -系统
    -Linux
---

## 前言

考研之前就一直想装黑苹果,考完之后一顿折腾,每次进入安装界面都找不到磁盘,试了很多办法都不能奏效,只能作罢.作为开发人员,就想安装linux作为主力系统了.一开始感觉linux会比较难,就安装了deepin,装完之后感觉不太折腾,就安装了大名鼎鼎的[majaro](https://manjaro.org/),美观有能折腾.

<!--more-->

## 下载工具

可以参考官网给出的[安装步骤](https://manjaro.org/support/firststeps/).
![lUnMa4.png](https://s2.ax1x.com/2020/01/03/lUnMa4.png)

### 下载系统镜像

进入官网可以找到镜像下载的地址[下载地址](https://manjaro.org/download/)

### 下载刻录工具

官方推荐[rufus](https://rufus.ie/),而且官方和大部分博客都推荐dd刻录模式,但是我没找到,直接就刻录到U盘了,亲测可以安装成功.

## 安装系统

### 进入安装程序

    注意!!!最好是断网安装.
进入BIOS修改启动项,讲U盘的UEFI放到第一个,接着就可以进入安装系统的程序.

        注意!!!!!双显卡的电脑一般会卡在
        1 watchdog: BUG: soft lockup -CPU#1 stuck for 23s![kworker/1:2:239]
        2 Started TLP system startup/shutdown
        3 A start job is running for livemedia mhwd scripe(xxxx)

#### 修复办法

- 引导盘开机看到启动菜单的时候，用方向键移到BOOT那一栏。
- 按E进入编辑，将 driver=free 改成 driver=intel
- 并在其后面加上 xdriver=mesa acpi_osi=! acpi_osi="Windows 2009"
- 然后按 Ctrl+X 或者 F10启动。

### 分区建议

我是128G固态+1TB机械的硬盘,其中300G用来安装Windows,剩下的全部用来装manjaro.将要安装的硬盘全部删除,在进行挂载.

        注意!!!双系统一定要注意Windows的efi分区,七九不小心删除了,进不去了.

- /home用剩下的600G机械挂载,文件系统为ext4
- /boot用512M固态挂载,,文件系统为ext4
- /boot/efi用512M固态挂载,文件系统为fat32
- swap交换空间用8GB固态挂载
- /usr用10GB固态挂载,文件系统为ext4
- /  用剩余全部固态挂载,文件系统为ext4

接下来基本上都是下一步即可.

## 安装后的配置

### 配置国内源

- 更改manjaro的国内源

```bash
sudo pacman-mirrors -i -c China -m rank
sudo pacman -Syy
```

- 设置archlinux国内源

        [archlinuxcn]
        SigLevel = Optional TrustedOnly
        Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
- 配置完成后,执行下列命令

```bash
sudo pacman -Syy  
sudo pacman -S archlinuxcn-keyring
```

### pacman替代命令yay

```bash
sudo pacman -S yay
```

yay 的命令参数跟pacman参数基本一致。

### 安装搜狗输入法

```bash
sudo pacman -S fcitx-im
sudo pacman -S fcitx-configtool
sudo pacman -S fcitx-sogoupinyin
```

添加输入法配置文件 sudo vim ~/.xprofile(没有就在主目录下创建一个,vim不行就用nao)

    export GTK_IM_MODULE=fcitx
    export QT_IM_MODULE=fcitx
    export XMODIFIERS="@im=fcitx"

### 其他软件

- 微信 sudo pacman -S electronic-wechat yay -S deepin-wine-wechat
- 百度网盘 sudo pacman -S baidunetdisk-bin
- VisualStudioCode sudo pacman -S visual-studio-code-bin
- 网易云音乐 sudo pacman -S netease-cloud-music
- 深度截图 sudo pacman -S deepin-screenshot
- 深度画板 sudo pacman -S deepin-draw
- 深度录屏 sudo pacman -S deepin-screen-recorder
- WPS  sudo pacman -S wps-office和sudo pacman -S ttf-wps-fonts