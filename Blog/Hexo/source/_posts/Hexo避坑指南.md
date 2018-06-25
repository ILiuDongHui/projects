---
title: Hexo避坑指南
comments: true
categories:
  - Hexo
tags:
  - Hexo
date: 2018-05-29 13:00:00
updated:
---
搭建基于 Hexo + GitHub Pages 的静态个人博客网站，记录此间遇到的坑，献给此刻正在迷茫而不知所措的你。
<!-- more -->

*PS：此教程仅适用于windows，其他操作系统请自行查阅资料*

## Git 下载缓慢
如果不翻墙，直接从Git官网下载，速度有时会慢到你吃惊…
建议：  
1.下载广大网友给出的资源（可联系作者索取）
2.下载翻墙软件，通过翻墙来增加下载速度
（推荐Lantern，免费500MB/月，简单快捷，可联系作者索取）

## Windows 安装好 Git 之后，使用 hexo init 命令，提示 git 命令错误
原因是在 hexo init 初始化的网站目录，没有建立 Git 仓库，需要使用 git init 命令建立 Git 仓库

## 部署到 GitHub，无法提交到 GitHub
GitHub 设置中，邮箱设置了阻止推送，关闭即可

## 部署到 GitHub，页面 CSS 样式失效
本地一切正常，部署到GitHub上，所有的样式和脚本全失效。  
解决方案：  
只需要自定义一个顶级域名，并解析到 YourRepositoryName.io 这个仓库上，域名解析到 GitHub Pages 教程请参考我的另一篇博客 {% link 更换GitHubPages域名 http://blog.ildh.net/2018/06/22/更换-GitHub-Pages-域名/ %}，可购买域名，阿里云、腾讯云等都是不错的商家，域名也比较便宜，然后到GitHub进入你的仓库，点击Settings，一直往下翻，找到GitHub Pages，
在 Custom domain 的文本框中输入你购买的域名，此时会在你的仓库生成一个CNAME文件，并且在浏览器输入购买的域名，即可看到样式生效后的网站。  
注意：CNAME文件在GitHub Pages设置 Custom domain 的时候生成了一次，但是本地的hexo的souce目录下没有该文件，因此在你使用hexo d -g的时候会自动将CNAME文件删除。  
如何解决呢？只需要将这个 CNAME 文件从 GitHub 中下载下来，放到 source 目录中，使用 hexo d -g 命令时就会自动将这个文件传上去。

## Hexo部署报错
使用命令 hexo d -g 发布到 GitHub 时，报下面这个错： 
```bash
Deployer not found: git
```
是因为没有装hexo-deployer-git这个插件,在hexo站点目录，输入以下命令安装：
```bash
npm install hexo-deployer-git --save
```
