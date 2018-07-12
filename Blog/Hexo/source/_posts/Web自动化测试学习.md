---
title: Web自动化测试学习
comments: true
categories:
  - 测试
tags:
  - 自动化测试
  - Python
  - Node.js
  - Selenium
date: 2018-07-10 12:48:52
updated:
---
![](http://pbedarn4e.bkt.clouddn.com/image/png/Selenium_Webdriver.png)
<!-- more -->

前短时间看到测试的同事在用 `Python` 写自动化测试，自己虽然是开发，但对自动化测试还是很感兴趣的，有时候自己要测一个功能的时候，需要登录，然后点击菜单，还要点击按钮等等一系列的操作，很费时且低效，希望能够写一点简单的自动化测试代码帮助自己减少不必要的操作的想法，再加上前两天看了点 `Python` 的教程，试着在网上找了个自动化测试的示例，并且能够写一些简单的测试脚本，所以记录在此，方便下次查找。

# 框架
这里使用的是 `Selenium3.0` Web测试框架，这个框架支持了多种编程语言和脚本语言，`Java、C#、JavaScript`等等。  
官方网站国内无法访问，需要翻墙，地址：[https://www.seleniumhq.org/](https://www.seleniumhq.org/)  
翻墙推荐 [Lantern（蓝灯）](https://github.com/getlantern/download/)

# WebDriver
`Selenium` 需要使用 `WebDriver`  

Browser（浏览器）|Component（组件）
-|:-:|-:
Chrome |[Chromedriver.exe](http://chromedriver.storage.googleapis.com/index.html)
Internet Explorer |[IEDriverServer.exe](http://selenium-release.storage.googleapis.com/index.html)
Edge |[MicrosoftWebDriver.msi](http://go.microsoft.com/fwlink/?LinkId=619687)
Firefox 47+ |[geckodriver(.exe)](https://github.com/mozilla/geckodriver/releases/)
PhantomJS |[phantomjs(.exe)](http://phantomjs.org/)
Opera |[operadriver(.exe)](https://github.com/operasoftware/operachromiumdriver/releases)
Safari |[SafariDriver.safariextz](http://selenium-release.storage.googleapis.com/index.html)
  
把这些驱动下载，并存放到一个目录中，例如 `D:/driver/` ，然后，把这这个目录添加到系统环境变量 `path` 下面。  


# Python3 + Selenium3.0
`Python` 是现在比较火的一门脚本语言，易学易用。

## Windows 下安装 Python3
`Python` 下载地址：[https://www.python.org/downloads/](https://www.python.org/downloads/)  
下载以后，点击运行开始安装，点击 `next` 直到 `finish`  
`Python3` 不需要配置环境变量就可以直接在命令行使用

## 用 Python 安装 Selenium3.0  
`Selenium` 可以使用 `Python` 的 `pip` 命令安装扩展库。  
`pip` 是一个安装和管理 `Python` 包的工具，安装 `Python` 时就自动安装好了
在 `Windows` 命令行输入 `pip` 出现说明信息，说明可以正常使用  
`Selenium 2.x` 已经升级到 `Selenium3.x` ，所以我们下载最新版就好
```bash
# 安装命令（找不到对应的版本，pip 会下载默认的版本）
pip install selenium==3.0

# 卸载命令
pip uninstall selenium
```

## 测试示例
```python
#coding=utf-8

#第一句表示代码的编码格式是uft-8格式，方便添加中文注释等

# 导入 selenium 的 webdriver 包，只有导入 webdriver 包我们才能使用 webdriver API 进行脚本的开发
from selenium import webdriver

# 实例化一个 Chrome浏览器 的驱动对象（即打开浏览器）
driver=webdriver.Chrome()

# 窗口最大化
driver.maximize_window()

# 定义一个变量，接收我们要访问的网站的网址
first_url='http://www.baidu.com'

# 使用 GET 方法访问网址
driver.get(first_url)

# 在 python 的输出窗口打印一句话（访问某某某网址，可有可无）
print ("access to %s " %(first_url))

# 找到网页上 id 为 kw 的 HTML 标签，并设置它的值是 "hello world"
driver.find_element_by_id("kw").send_keys("hello world")

# 找到网页上 id 为 su 的 HTML 标签，并点击它
driver.find_element_by_id("su").click()

# 关闭浏览器（如果开启这句话，浏览器会执行完脚本后自动关闭，测试时可关闭这句）
# driver.quit()
```

# NodeJS + Selenium3.0
在用 `Python` 以后发现似乎 `JavaScript` 也可以做自动化测试，因为 `Selenium` 支持 `JavaScript` ，所以我又上网搜索资料，果然发现可以使用 `NodeJS` + `Selenium` 进行自动化测试，和上面用 `Python` 差不多。

## Windows 下安装 NodeJS
`NodeJS` 下载地址： [https://nodejs.org/en/](https://nodejs.org/en/)  
下载完成，点击安装，一直到安装完成。  

## 用 NodeJS 安装 Selenium
`Selenium` 可以通过 `npm` 安装。（ `npm` 是随同 `NodeJS` 一起安装的包管理工具。）

```bash
# 安装命令
npm install selenium-webdriver

# 卸载命令
npm uninstall selenium-webdriver
```

## 测试示例
当 `Selenium-webdriver` 被 `npm` 下载完成，将到在当前目录下多出一个 `./node_modules/`目录。然后，在与这个目录同级的目录下创建第一个 `Selenium` 测试脚本 `baidu.js` 。  
```javascript
// 导入 selenium-webdriver 组件，并获取 By 和 until 两个对象
var webdriver = require('selenium-webdriver'),
    By = webdriver.By,
    until = webdriver.until;

// 实例化
var driver = new webdriver.Builder()
    .forBrowser('chrome')
    .build();

// 打开百度
driver.get('https://www.baidu.com');

// 通过 id，找到搜索文本框元素，并输入文字 'webdriver'
driver.findElement(By.id('kw')).sendKeys('webdriver');

// 通过 id，找到搜索按钮，并点击它
driver.findElement(By.id('su')).click();

// 等待1秒钟（1000毫秒=1秒），设置搜索结果的网页标题为 'webdriver_百度搜索'
driver.wait(until.titleIs('webdriver_百度搜索'), 1000);

// 关闭浏览器
driver.quit();
```
这段代码的作用和上班的示例是一样的，就不再赘述。  
在 `bandu.js` 文件所在目录，按住 `shift` 键，用鼠标右键点击空白处，选择 `在此处打开 Powershell 窗口` 即可在命令行打开当前目录，输入一下命令：
```bash
node baidu.js
```


# 注意事项
1. 在自己编写其他网站的脚本时，发现会获取不到页面元素，即 `HTML` 标签，那是因为网页使用了 `frame` 这个标签，那么我们可以使用 `driver.switch_to.frame(frame name)` 方法切换到相应的 `frame`，然后就可以获取到这个 `frame` 里面的元素了。

`>>> Python`
```python
# 切换到某个frame
switch_to.frame('frame id/name') 
# 切换到第几个frame，从0开始
switch_to.frame(0) 

# 切换到父级frame
switch_to.parent_frame()

# 切换到主文档
switch_to.default_content()
```

`>>> NodeJS`
```javascript
// 切换到某个frame
switchTo().frame('frame id/name') 
// 切换到第几个frame，从0开始
switchTo().frame(0) 

// 切换到父级frame
switchTo().parentFrame()

// 切换到主文档
switchTo().defaultContent()

// 获取 frame 的 src 属性，并打开这个地址
String URL = driver.findElement(By.id("Frame Id")).getAttribute("src").toString();
driver.get(URL);
```
`NodeJS` 语法和 `Python` 语法不同，需要注意某些方法名称是否正确。  

2. 可能出现打开浏览器后，闪退的情况，或者打开浏览器后，地址栏没有自动输入并跳转网址，这时候我们检查一下 `webdriver` 的版本，如果版本太低，就去先前的地址下载高版本的就行了。

# 异常

## 报错 selenium.common.exceptions.NoSuchFrameException: Message: no such frame 无法切换 frame
错误信息：`selenium.common.exceptions.NoSuchElementException: Message: no such element: Unable to locate element`
错误原因: 所在的框架不对 导致找不到元素  
解决方法: 1. 先回到最外层框架 2.进入要定位元素的框架 3.定位  
```python
driver.switch_to.default_content()	# 回到主框架
driver.switch_to_frame("xxx")		# 进入要定位元素被包含的那层框架,框架可以用id和name直接定位
driver.find_element_by_xpath('xxx')	# 用xpath定位
```


# End