---
title: 更换 GitHub Pages 域名
date: 2018-05-29 20:00:00
categories: 
- GitHub
tags:  
- GitHub Pages
comments: true
---
{% asset_img github_pages.png %}
<!-- more -->

## Begin
对于在下这种特困户，是不会自己去花钱搭建服务器的，`GitHub` 提供了一个免费的网站托管空间，可以用来托管自己的博客之类的。  
前面讲了怎么搭建 `GitHub Pages` 博客，已经可以使用 `repo.io` 进行访问了，但是这个 `RepositoryName.github.io` 域名，作为程序员来说，还是比较好记的，但是对于普通人来说，真的就不太友好了，就是不好记。  

### 第一步：GitHub Pages 绑定自定义域名（Custom domain）
1. 首先进入你的博客repo，找到右边的 `Settings`  
2. 往下滚动，找到 `GitHub Pages`  
3. 修改 `Source` 选项为 `master branch` ,点击保存
4. 刷新页面，再次找到 `GitHub Pages` ，会看到 `Custom domain` ，在下边的输入框中，输入你的域名，点击保存
5. 为了让这个域名长久有效，可在你的仓库里创建一个名为 `CNAME` 的文件（没有后缀名），内容写入你的域名
6. 这样 `GitHub Pages` 单方面设置就完成了

### 第二步：个人域名绑定
现在以阿里云购买的域名为例  
在阿里云的域名解析里，给域名添加一条 `A` 记录的解析

记录类型|主机记录|解析线路|记录值|MX优先级|TTL|状态
:-:|:-:|:-:|:-:|:-:|:-:|:-:
A|www|默认|192.30.252.153|--|10分钟|正常
CNAME|@|默认|repo.io|--|10分钟|正常

`192.30.252.153` 是 `Github Pages` 服务器指定的 `IP` 地址，访问该 `IP` 地址即表示访问 `Github Pages` 
此时，你的个人域名就绑定到了你的 `GitHub Pages` 域名 `repo.io` 上了，可以通过 `http://你的域名` 访问了

### 附加：二级域名绑定
上面完成后，要绑定二级域名就很简单了，在 `GitHub Pages` 中修改 `Custom domain` 以及修改 `CNAME` 文件的内容为你的二级域名地址，再回到阿里云域名解析中，增加一条二级域名解析：

记录类型|主机记录|解析线路|记录值|MX优先级|TTL|状态
:-:|:-:|:-:|:-:|:-:|:-:|:-:
A|www|默认|192.30.252.153|--|10分钟|正常
CNAME|@|默认|repo.io|--|10分钟|正常
CNAME|blog|默认|repo.io|--|10分钟|正常

至此，就可以通过 `http://blog.你的域名` 进行访问了
## End