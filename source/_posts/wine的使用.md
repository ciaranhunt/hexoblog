---

title: 安装hexo
date: 2019-12-31 18:10:24
categories:
    -技术向
tags:
    -hexo

---

## 使用wine

linux运行Windows程序

<!--more-->

## 运行/安装Windows应用

```bash
wine <exe文件>
msiexec -i <msi安装包>
```

## wine菜单管理

Wine中安装的应用可以在系统菜单中以Wine子菜单的形式呈现，给予打开应用的便利。例如在系统菜单中的WeChat启动项：
这一启动项在文件系统中的存储位置是~/.local/share/applications/wine/Programs/WeChat/WeChat.desktop
其内容为：

```text
#文件内容:
[Desktop Entry]
Encoding=UTF-8
Name=eclipse
Comment=The Java IDE for Java Developers
Exec=/opt/eclipse/eclipse %F
Path=/opt/eclipse
Icon=/opt/eclipse/icon.xpm
Terminal=false
Type=Application
Categories=Application;Programme;
```

```text
语法解释：
关键词                         意义
[Desktop Entry]               文件头
Encoding                      编码
Name                          应用名称
Name[xx]                      不同语言的应用名称
GenericName                   描述
Comment                       注释
Exec                          执行的命令
Icon                          图标路径
Terminal                      是否使用终端
Type                          启动器类型
Categories                    应用的类型（内容相关）

说明： 
其中 Exec 常用的参数有：%f %F %u %U 
%f：单个文件名。即使选择了多个文件。如果已选择的文件不在本地文件系统中（比如说在HTTP或者FTP上），这个文件将被作为一个临时文件复制到本地，％f将指向本地临时文件； 
%F：文件列表。用于程序可以同时打开多个本地文件。每个文件以分割段的方式传递给执行程序。 
%u：单个URL。本地文件以文件URL或文件路径的方式传递。 
%U：URL列表。每个URL以分割段的方式传递给执行程序。本地文件以文件URL或文件路径的方式传递。
修改权限:
chmod 755 test.desktop
路径:/usr/share/applications/
```

Wine安装应用时一般会添加这个菜单，如果没有的话可以在~/.local/share/applications/wine/下新建目录和.desktop文件，按[Desktop Entry]的格式自行设置。
