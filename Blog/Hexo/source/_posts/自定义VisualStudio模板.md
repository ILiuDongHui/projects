---
title: 高效 .NET 开发之自定义 Visual Studio 模板
comments: true
date: 2018-06-22 18:12:58
updated:
categories:
  - IDE
tags:
- .NET
- C#
- Visual Studio
---
{% asset_img visualstudio2010.png %}
<!-- more -->

&#160; &#160; &#160; &#160;学习开发的时候，往往我们只顾着写代码，很少注意到规范问题，但是在正式的工作中做项目的时候，每个公司几乎都有自己的代码规范，如：编写文档注释，以往常常是挨个 Copy 然后 Paste，然后每次需要改很多信息，如：Class文件名称，工程名称，创建时间等等，不仅浪费时间，而且降低效率，并且对于没有耐心的人来说，很容易出错。

## 内心的挣扎
既然如此，作为一个懒人，就想有没有办法自动增加这些固定的东西呢？答案自然是：有。

Visual Studio 其实在 `新建项目` 或者 `新建项` 的时候，都是使用的 .NET 提供的一些默认的模板，  
既然如此，那么我们就可以在这个模板上做文章咯。

## 方法一：修改 `项模板`
1. 打开 Visual Studio 安装目录，Windows 默认安装目录：  
`C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\ItemTemplates\`
在这个目录下，你将看到要创建各种类型的目录列表，打开你要设置的文件，  
如：CSharp\Code\2052\Class\ 目录下，如修改 Class.cs ，则当你新建一个 Class.cs 文件时，就会出现你定义好的模版。  
那么问题来了，怎么修改呢：
    打开 Class.cs 文件，你会看到 `$if` 等热词，这些在新建文件时会动态解析，把结果返回到新建文件中。  
    在新建 Class.cs 时我们想添加个人信息，就可以添加如下：
``` csharp
/* ======================================================================== 
* 【本类功能概述】 
*  
* 作者：ywg 时间：$time$ 
* 文件名：$safeitemname$ 
* 版本：V1.0.1 
* 
* 修改者	： 
* 时间	：  
* 修改说明： 
* ======================================================================== 
*/ 

// 有了这些，大大提高了效率，体现专业的水平。

// 下面是其他的参数：
$time$  //显示当前时间
$safeitemname$  //显示当前创建文件名
$safeprojectname$  //显示当前工程名
$year$  //显示当前年份
$projectname$  //当创建一个新 工程时，指定的工程名
$clrversion$  //当前CLR解析的版本值
$GUID [1-10]$  //定义当前范围的GUID  
```
  
## 方法二：导出 `项目模板`  
此方法，可以将预先创建好的项目，导出为一个项目模板，以便在后面用该模板创建项目。  
1. 新建一个项目（需要设置为模板的项目）。  
2. 在新建项目中，添加好自己的目录结构，编写好自己预设的 Class 文件。  
3. 在`文件`菜单中，选择`导出模板`。选择创建模板的类型（项目模板/项模板），以及模板所在的项目（你的工程），单击下一步。  
4. 然后按照提示步骤，填写模板名称，模板说明，图标图像，，最后选中`自动将模板导入 Visual Studio(A)`，单击`完成(F)`创建模板。  
5. 完成上述操作，即可在`新建项目`/`新建项`页面看到我们的模板。  
6. Visual Studio 默认导入模板是添加到了所属语言的根目录。键入我们想法与对应目录，比如`Web`中，打开用户模板文件夹，然后在其中新建`Web`文件夹，将模板移动到其中即可。  

## 总结
学习和工作是两回事，工作需要高效
{% blockquote %}
工欲善其事必先利其器  
{% endblockquote %}
尤其是『程序』员，首先就是要让自己不去做重复的事情，不要只知道 Copy & Paste，这又不是一件省力的事儿；遇到麻烦要学会如何解决麻烦，这就是学习进步的过程。  

## 参考文章 
1. [https://blog.csdn.net/wlj323/article/details/46955109](https://blog.csdn.net/wlj323/article/details/46955109)
