---
title: Sublime Text 3 激活教程
comments: true
categories:
  - IDE
tags:
  - 破解
  - 激活
  - 注册码
date: 2018-06-28 09:55:14
updated:
---
Sublime Text 在 2018年05月14日 已经更新至 3.1.1 Build 3176 版本，随之而来的是我们安装的 Sublime Text 3 激活状态又失效了，一起来看看如何激活最新版吧
{% asset_img sublimetext3.1.1build3176(unlimited).png %}
<!-- more -->

## Windows 激活 Sublime Text 3.1.1 Build 3176
### 修改 hosts 文件
1. 找到 windows 的 hosts 文件，文件路径：
```bash
C:\Windows\System32\drivers\etc\hosts
```
2. 用编辑器打开 hosts 文件，在最后加上两句
```bash
127.0.0.1		www.sublimetext.com
127.0.0.1		license.sublimehq.com
```
这里的 127.0.0.1 也可以替换为 0.0.0.0，都是可以的，注意有可能会出现修改后无法保存的问题，那是因为 hosts 文件是系统文件，编辑器没有修改权限，建议使用 Notepad++ 这款编辑器，它会提示你权限不足，是否提升为管理员权限进行修改保存。  
{% asset_img hosts_edit.png %}

### 移除旧的许可证
打开 Sublime Text 3 ，点击菜单栏 `Help > Remove License`
{% asset_img sublimetext3.1.1build3176(unregistered).png %}

### 输入新的许可证
```bash
----- BEGIN LICENSE -----
sgbteam
Single User License
EA7E-1153259
8891CBB9 F1513E4F 1A3405C1 A865D53F
115F202E 7B91AB2D 0D2A40ED 352B269B
76E84F0B CD69BFC7 59F2DFEF E267328F
215652A3 E88F9D8F 4C38E3BA 5B2DAAE4
969624E7 DC9CD4D5 717FB40C 1B9738CF
20B3C4F1 E917B5B3 87C38D9C ACCE7DD8
5F7EF854 86B9743C FADC04AA FB0DA5C0
F913BE58 42FEA319 F954EFDD AE881E0B
------ END LICENSE ------
```
完成，以下是主要截图
{% asset_img sublimetext3.1.1build3176(enter_license).png %}
{% asset_img sublimetext3.1.1build3176(purchasing).png %}
{% asset_img sublimetext3.1.1build3176(registered).png %}

## 结尾
PS：  
文中提到的编辑器 [Notepad++ 点击下载](https://notepad-plus-plus.org/) 
这里推荐一个 windows 文件快速搜索软件 [Everything 点击下载](http://www.voidtools.com/)
{% asset_img Everything.Search.Window.png %}