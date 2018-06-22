---
title: Hello World
date: 2018-05-28 15:58:21
categories: 
- 
tags:  
- Hexo
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).
<!-- more -->

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

### Block Quote（引用块）
在文章中插入引言，可包含作者、来源和标题。  
**别号**：quote
``` 
{% blockquote [author[, source]] [link] [source_link_title] %}
content
{% endblockquote %}
```

### Code Block（代码块）
在文章中插入代码。
```
{% codeblock [title] [lang:language] [url] [link text] %}
code snippet
{% endcodeblock %}
```

### Image（相对路径引用的标签插件）
```
{% img [class names] /path/to/image [width] [height] [title text [alt text]] %}

example：
{% asset_img example.jpg This is an example image %}
```
More info: [Deployment](https://hexo.io/docs/deployment.html)
