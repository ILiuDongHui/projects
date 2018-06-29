---
title: NexT主题美化
comments: true
categories:
  - Hexo
tags:
  - NexT
  - Hexo
date: 2018-05-29 19:30:00
updated:
---
# 前言
{% asset_img next.png %}
<!-- more -->
可美化的内容大致如下：
* 主题美化
 * 开启`CC BY-NC-SA 3.0`协议
 * 更有用的公益404
 * 酷炫的动态背景
 * 鼠标点击特效
 * 旋转的圆形头像框
 * 修改链接文字样式
 * 修改代码块样式
 * 首页文章阴影效果
 * 网站顶部加载进度条
 * 网站底部的字数统计
* 使用第三方服务
 * 开启`Valine`评论系统（基于`LeanCloud`）
 * 开启`Gitment`评论系统（基于`GitHub`）
 * 开启`baidu_analytics`百度统计
 * 开启`Algolia`搜索服务
* Hexo博客插件
 * 开启`RSS`订阅
 * 设置站点导航`Sitemap`

# 主题美化

## 开启 CC BY-NC-SA 3.0 协议
打开`\themes\NexT\_config.yml`，找到`post_copyright`，设为`true`。

## 更有用的公益404
1. 在hexo站点source目录下，新建文件404.html
2. 打开`\themes\NexT\_config.yml`，找到 `menu` ,将 `commonweal` 前面的 # 删掉，修改路径为 /404.html，即可
3. 使用腾讯公益404页面替代自己的404页面，做点好事是很好的，只需要把下面这段代码覆盖到你的404.html里就可以了
``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>404</title>
</head>
<body>
    <script type="text/javascript" src="//qzonestyle.gtimg.cn/qzone/hybrid/app/404/search_children.js" charset="utf-8" homePageUrl="http://yoursite.com/yourpage.html" homePageName="回到我的主页"></script>
</body>
</html>
```

## 酷炫的动态背景
打开`\themes\NexT\_config.yml`，修改以下内容：
```yaml
# 背景特效以下4项，是NexT主题集成的，只需将 false 改为 true，即可启用
# 不用向网上说的，到模板文件里加引用js的脚本，NexT已经集成了，开启即用

# Canvas-nest 浮动线条
canvas_nest: false

# three_waves 水波粒子
three_waves: false

# canvas_lines 这个是一根线连接两个小点，组成的一个随鼠标放大缩小的东西
canvas_lines: false

# canvas_sphere 这个是一个很多刺组成的一个球
canvas_sphere: false
```

## 鼠标点击特效
待更新...

## 旋转的圆形头像框
修改 `themes\next\source\css\_common\components\sidebar\sidebar-author.styl`：
```css
.site-author-image {

  display: block;
  margin: 0 auto;
  padding: $site-author-image-padding;
  max-width: $site-author-image-width;
  height: $site-author-image-height;
  border: site-author-image-border-color;

  /* start*/
  border-radius: 50%
  webkit-transition: 1.4s all;
  moz-transition: 1.4s all;
  ms-transition: 1.4s all;
  transition: 1.4s all;
  /* end */

}

/* start */
.site-author-image:hover {

  background-color: #55DAE1;
  webkit-transform: rotate(360deg) scale(1.1);
  moz-transform: rotate(360deg) scale(1.1);
  ms-transform: rotate(360deg) scale(1.1);
  transform: rotate(360deg) scale(1.1);
}
/* end */
```

## 修改链接文字样式
打开`themes\next\source\css\_common\components\post\post.styl`添加以下代码：

``` css
.post-body p a{
 color: #0593d3;
 border-bottom: none;
 /*border-bottom: 1px solid #0593d3;*/	/*蓝色下划线*/
 &:hover {
   color: #fc6423;  					/*#ff106c;蓝色*/ /*#fc6423;橘红色*/
   /*text-decoration: underline;*/		/*超链接下划线*/
   border-bottom: none;
   border-bottom: 1px solid #fc6423;	/*橘红色下划线*/
 }
}
```

## 修改代码块样式
打开`\themes\NexT\source\css\_custom\custom.styl`，增加样式选择器：
（具体样式可自定义）
```css
// 行代码块解析的Html标签是<code>some code...</code>
// 行代码块样式
code {
    color:#ff7600;
    background:#fbf7f8;
    margin:2px;
 }

// 多行代码块解析的Html标签是<pre><code>some code...</code></pre>
// 多行代码块自定义样式
.highlight, pre{
  margin:5px 0;
  padding:5px;
  border-radius:3px
}
.highlight, code, pre{
  border:1px solid #d6d6d6;
}
```

## 主页文章添加阴影效果
打开`themes/next/source/css/_custom/custom.styl`文件添加：
``` css
.post {
   margin-top: 60px;
   margin-bottom: 60px;
   padding: 25px;
   -webkit-box-shadow: 0 0 5px rgba(202, 203, 203, .5);
   -moz-box-shadow: 0 0 5px rgba(202, 203, 204, .5);
  }
```

## 启用：页面加载过程中顶部的进度条
打开`\themes\NexT\_config.yml`，找到字段 `pace` ，设为 true。

## 启用：字数统计
```bash
# 执行此命令，安装NexT以来插件
npm i --save hexo-wordcount
```
打开`\themes\NexT\_config.yml`，找到 `post_wordcount` 属性，
```yaml
# Post wordcount display settings   文章字数显示设置
# Dependencies: https://github.com/willin/hexo-wordcount    依赖hexo-wordcount插件。安装命令 "npm install --save hexo-wordcount"
post_wordcount:
  item_text: true
  wordcount: false    # 设为 true，开启 字数统计      （文章标题下面）
  min2read: false     # 设为 true，开启 阅读时长≈     （文章标题下面）
  totalcount: false   # 设为 true，开启 全站字数统计   （网站底部，版权声明的右侧）
  separated_meta: true
```

# 使用第三方服务
## 评论系统
### Valine
1. 登陆 LeanCloud，创建应用，创建一个新的Class，命名为Comment
2. 打开`\themes\NexT\_config.yml`，找到字段 `valine` 
3. 将 `appid` 值设置成你的 LeanCloud 的 App ID，
4. 将 `appkey` 的值设置成你的 LeanCloud 的 App key 
5. 将 `enable` 的值设置成 true
6. 将 `placeholder` 的值设置成你想要的评论提示语

### Gitment
[参考文档](https://imsun.net/posts/gitment-introduction/)  
1. 准备:   
Gitment 需要一个 GitHub 仓库用来存储评论数据,  
需要注册一个开发账号.[点击注册](https://github.com/settings/applications/new)  
2. 打开`\themes\NexT\_config.yml`，找到 "Gitment"  
由于我的版本和参考文档中的不一致,所以配置文件中的属性也不一样,我的配置如下
```yaml
# Gitment       # Gitment 评论系统（目前在用）
# Introduction: https://imsun.net/posts/gitment-introduction/
# You can get your Github ID from https://api.github.com/users/<Github username> 
gitment:
  enable: true    # 是否启用（默认false）
  mint: true      # 这句没看懂,不用管,默认就行
  count: true     # 显示评论计数（默认true）
  lazy: false     # 评论用按钮加载懒惰（默认false）,false就直接展示评论,true就显示一个查看评论按钮
  cleanly: true   # 隐藏页脚的 'Powered by ...' 字样（默认false）
  language:       # 这里可以不填
  github_user:    # 必填.这里填入你的 GitHub ID，就是你的Github登陆用户名,区分大小写
  github_repo:    # 必填.用于存储 Gitment 评论的仓库名称,区分大小写
  client_id:      # 第一步中注册后，会看到有client id 和client secret
  client_secret:  # 第一步中注册后，会看到有client id 和client secret
  proxy_gateway:  # 不管
  redirect_protocol: # 不管
```
3. 完成以后,在文章最后,用GitHub账号登陆,即可评论

## 数据统计与分析
### 百度统计
{% blockquote %}
注意： baidu_analytics 不是你的百度 id 或者 百度统计 id
{% endblockquote %}
1. 登录 <font style="color: blue;">{% link 百度统计 https://tongji.baidu.com/web/welcome/login %}</font>， 定位到站点的代码获取页面
2. 创建应用，定位到站点的代码获取页面
3. 复制 hm.js? 后面那串统计脚本 id，如：
{% asset_img analytics-baidu-id.png %}
4. 打开`\themes\NexT\_config.yml`， 修改字段 `baidu_analytics` 字段，值设置成你的百度统计脚本 id。

### 阅读次数统计（LeanCloud）
请查看 {% link 为NexT主题添加文章阅读量统计功能 https://notes.wanghao.work/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%85%8D%E7%BD%AELeanCloud %}

## 搜索服务
### Algolia 搜索
1. 注册 Algolia，创建 Index
前往 {% link Algolia https://www.algolia.com %} 注册页面，注册一个新账户。 可以使用 GitHub 或者 Google 账户直接登录，注册后的 14 天内拥有所有功能（包括收费类别的）。之后若未续费会自动降级为免费账户，免费账户 总共有 10,000 条记录，每月有 100,000 的可以操作数。注册完成后，创建一个新的 Index，这个 Index 将在后面使用。
2. 安装 Hexo Algolia
``` bash
# cd 到 hexo 站点根目录下，执行

npm install --save hexo-algolia
```
3. 获取 Key，更新站点配置
在 Algolia 服务站点上找到需要使用的一些配置的值，包括 ApplicationID、Search-Only API Key、 Admin API Key。注意，Admin API Key 需要保密保存。点击ALL API KEYS 找到新建INDEX对应的key， 编辑权限，在弹出框中找到ACL选择勾选Add records, Delete records, List indices, Delete index权限，点击update更新。  
编辑 <font style="background-color: #9954BB;color:#fff;">站点配置文件</font>，新增以下配置：
``` yaml
algolia:
  applicationID: 'applicationID'
  indexName: 'indexName'
  chunkSize: 5000
```
替换除了 chunkSize 以外的其他字段为在 Algolia 获取到的值。  
（注意：是站点配置文件，不是主题配置文件）
4. 更新 Index
当配置完成，在站点根目录下执行
``` bash
$ export(windows 为 set) HEXO_ALGOLIA_INDEXING_KEY=Search-Only API key
$ hexo algolia
```
来更新 Index。请注意观察命令的输出。
{% asset_img algolia-step-4.png %}
5. 主题集成
更改<font style="background-color: #9954BB;color:#fff;">主题配置文件</font>，找到 Algolia Search 配置部分：
``` yaml
# Algolia Search
algolia_search:
  enable: false
  hits:
    per_page: 10
  labels:
    input_placeholder: Search for Posts
    hits_empty: "We didn't find any results for the search: ${query}"
    hits_stats: "${hits} results found in ${time} ms"
```
将 enable 改为 true 即可，根据需要你可以调整 labels 中的文本。

# 插件

## RSS

## Sitemap