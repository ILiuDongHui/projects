---
title: NexT主题美化
comments: true
categories:
  - Hexo
tags:
  - NexT
  - Hexo
date: 2018-06-22 21:19:24
updated:
---
记录下此间过程，同时给路过的朋友参考一下
<!-- more -->

# 常规功能
## 404页面
1. 在hexo站点source目录下，新建文件404.html
2. 编辑 <font style="background-color: #9954BB;color:#fff;">主题配置文件</font>，找到 `menu` ,将 `commonweal` 前面的 # 删掉，修改路径为 /404.html，即可
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

### 美化站点特效
1. 增加动态背景
2. 增加鼠标点击弹出图标
3. 把侧边栏头像变成圆形，并且鼠标停留在上面发生旋转效果
修改 `themes\next\source\css\_common\components\sidebar\sidebar-author.styl`：
``` css
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
4. 修改连接文字样式：
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
5. 为next主题的主页文章添加阴影效果
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

# 第三方服务
## 评论系统
### Valine
1. 登陆 LeanCloud，创建应用，创建一个新的Class，命名为Comment
2. 编辑 <font style="background-color: #9954BB;color:#fff;">主题配置文件</font>，找到字段 `valine` 
3. 将 `appid` 值设置成你的 LeanCloud 的 App ID，
4. 将 `appkey` 的值设置成你的 LeanCloud 的 App key 
5. 将 `enable` 的值设置成 true
6. 将 `placeholder` 的值设置成你想要的评论提示语

## 数据统计与分析
### 百度统计
{% blockquote %}
注意： baidu_analytics 不是你的百度 id 或者 百度统计 id
{% endblockquote %}
1. 登录 <font style="color: blue;">{% link 百度统计 https://tongji.baidu.com/web/welcome/login %}</font>， 定位到站点的代码获取页面
2. 创建应用，定位到站点的代码获取页面
3. 复制 hm.js? 后面那串统计脚本 id，如：
{% asset_img analytics-baidu-id.png %}
4. 编辑 <font style="background-color: #9954BB;color:#fff;">主题配置文件</font>， 修改字段 `baidu_analytics` 字段，值设置成你的百度统计脚本 id。

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