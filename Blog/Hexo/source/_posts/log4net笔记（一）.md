---
title: log4net笔记（一）
date: 2018-06-22 16:33:30
categories:
- DotNet
tags:  
- CSharp
- Log
comments: true
---
&#160; &#160; &#160; &#160;**Apache log4net** 库是帮助程序员将日志语句输出到各种输出目标的工具。
log4net是Microsoft®.NET运行时的优秀Apache log4j™框架的一个端口。我们保持框架与原始log4j类似，同时利用.NET运行时的新功能。
<!-- more -->
# log4net 学习笔记-第一章
*作为一个程序员，要有一颗“活到老，学到老”的心，更何况现在还是个菜鸟，缺乏的技能点太多，总是有无尽的烦劳。*

还有整整一个月，毕业即将满1年了，可是技术还是那么菜，感生活不易，但仍要继续；
在小哥哥的第一个公司里苦干了一年多，忙于改BUG，什么都没学到，就连一个程序需要记录日志这种低级问题都不知道，  
属实不能忍，幸好小哥哥有一颗刨根问底儿的心。

### 什么是Apache log4net™
{% asset_img apache_logging.png %}
{% blockquote @Apache http://logging.apache.org/log4net/index.html Apache log4net 官方文档 %}
Apache log4net 库是帮助程序员将日志语句输出到各种输出目标的工具。log4net是Microsoft®.NET运行时的优秀Apache log4j™框架的一个端口。我们保持框架与原始log4j类似，同时利用.NET运行时的新功能。
{% endblockquote %}

简而言之，就是在.NET下，帮助程序员记录程序日志的东西，已经写的相当好的东西，拿来配置下就可以用的东西，比你自个儿写的日志要厉害很多的东西。  

### log4net简单示例-四步走
1. 不管你是什么程序，ConsoleApplication 也好，WebApplication 也好，都要写log4net的配置。  
{% link 参考地址 http://logging.apache.org/log4net/release/config-examples.html %}
在控制台中，需要新建一个 `.config` 类型的配置文件，里面有几个节点  
``` xml 
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
	<configSections>
    	<section name="log4net" type="log4net.Config.Log4NetConfigurationSectionHandler,log4net"/>
  	</configSections>

  	<log4net>
	  	<root>
	      <!--需要记录的日志级别-->
	      <!--<level value="FATAL"/>-->
	      <!--<level value="ERROR"/>-->
	      <!--<level value="DEBUG"/>-->
	      <!--<level value="WARN"/>-->
	      <!--<level value="INFO"/>-->
	      <level value="ALL"/>

	      <!--用哪个就开启哪个，不用就注释掉-->
	      <appender-ref ref="AdoNetAppender"/>
	      <!--<appender-ref ref="RollingLogFileAppender"/>-->
	    </root>

	    <!-- 若干 appender-->
		<!--RollingLogFileAppender写入文件-->
	    <appender name="RollingLogFileAppender" type="log4net.Appender.RollingFileAppender">
	      <!--日志写入指定文件-->
	      <file value="../../RuntimeError.log"/>
	      <!--每次记录过程开始时，文件将被附加到而不是被覆盖。-->
	      <appendToFile value="true"/>
	      <rollingStyle value="Size"/>
	      <!--备份log文件的个数最多10个-->
	      <maxSizeRollBackups value="10"/>
	      <!--单个log文件最大容量2MB，超过2MB将重新创建新的log文件，并将原来的log文件备份-->
	      <maximumFileSize value="100kb"/>
	      <staticLogFileName value="true"/>
	      <layout type="log4net.Layout.PatternLayout">
	        <!--1.用这个的话，日志只会写入 日志信息 ，其他的内容不会写入-->
	        <!--<file type = "log4net.Util.PatternString" value = "log-file  -  [%processid] .txt" />
	        <layout type = "log4net.Layout.PatternLayout" value = "%date [%thread]%-5level%logger  - %message%newline" />-->

	        <!--2.这俩加上后，会在每次写入的日志信息前加上 [Header]，结尾加上 [Footer]-->
	        <!--<header value="[Header]&#13;&#10;" />
	        <footer value="[Footer]&#13;&#10;" />-->
	        <conversionPattern value="%newline%date [%thread] %-5level %logger - %message%newline" />
	        
	        <!--3.最简洁的日志模板-->
	        <!--<conversionPattern value = "%newline%date  |  [%thread]  |  %-5level  |  %logger  |  [%property]  |   %message%newline" />-->
	      </layout>
	    </appender>

		<!--存放到 MS SQL Server 数据库（Apache官方配置示例）-->
	    <appender name="AdoNetAppender" type="log4net.Appender.AdoNetAppender">
	      <!--BufferSize为缓冲区大小，设置为0表示立即写入，生产环境一般设为10~100，然后一块写入数据库-->
	      <bufferSize value="0" />
	      <!--Ado.Net连接类型。这里是 SqlConnection-->
	      <connectionType value="System.Data.SqlClient.SqlConnection, System.Data, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
	      <!--数据库连接字符串-->
	      <!--<connectionString value="data source=[database server];initial catalog=[database name];integrated security=false;persist security info=True;User ID=[user];Password=[password]" />-->
	      <connectionString value="data source=.;initial catalog=MyDB;integrated security=false;persist security info=True;User ID=sa;Password=123" />
	      <!--插入日志记录SQL语句。-->
	      <!--数据库表定义:这里建议不用Log为表名，因为Log是sqlserver函数关键字
	      CREATE TABLE [dbo].[ErrorLog] (
	        [Id] [int] IDENTITY (1, 1) NOT NULL,
	        [Date] [datetime] NOT NULL,
	        [Thread] [varchar] (255) NOT NULL,
	        [Level] [varchar] (50) NOT NULL,
	        [Logger] [varchar] (255) NOT NULL,
	        [Message] [varchar] (4000) NOT NULL,
	        [Exception] [varchar] (2000) NULL
	      )
	      -->
      	<commandText value="INSERT INTO [dbo].[ErrorLog] ([Date],[Thread],[Level],[Logger],[Message],[Exception]) VALUES (@log_date, @thread, @log_level, @logger, @message, @exception)" />
      	<!--定义log4net参数。（%开头的是log4net自有参数，@开头的是配置中定义的参数）-->
      	<parameter>
	        <parameterName value="@log_date" />
	        <dbType value="DateTime" />
	        <layout type="log4net.Layout.RawTimeStampLayout" />
	      	</parameter>
      	<parameter>
	        <parameterName value="@thread" />
	        <dbType value="String" />
	        <size value="255" />
	        <!--模板可以自定义，需要继承 log4net.Layout.LayoutSkeleton-->
	        <layout type="log4net.Layout.PatternLayout">
	          <conversionPattern value="%thread" />
	        </layout>
      	</parameter>
      	<parameter>
	        <parameterName value="@log_level" />
	        <dbType value="String" />
	        <size value="50" />
	        <layout type="log4net.Layout.PatternLayout">
	          <conversionPattern value="%level" />
	        </layout>
      	</parameter>
	    <parameter>
	        <parameterName value="@logger" />
	        <dbType value="String" />
	        <size value="255" />
	        <layout type="log4net.Layout.PatternLayout">
	          <conversionPattern value="%logger" />
        	</layout>
      	</parameter>
      	<parameter>
        	<parameterName value="@message" />
        	<dbType value="String" />
        	<size value="4000" />
        	<layout type="log4net.Layout.PatternLayout">
          	<conversionPattern value="%message" />
        	</layout>
      	</parameter>
      	<parameter>
        	<parameterName value="@exception" />
        	<dbType value="String" />
        	<size value="2000" />
        	<layout type="log4net.Layout.ExceptionLayout" />
      	</parameter>
    	</appender>

  	</log4net>
</configuration>
```

这是最简单的配置，包含 `RollingLogFileAppender 写入文件` 和 `写入 SQL Server 数据库`  

2. 引用 log4net.dll 

3. 在工程的 `AssemblyInfo.cs` 文件中，引入 `log4net`  ，即追加以下信息：  
``` csharp
// 控制台和windows窗体：
[assembly: log4net.Config.XmlConfigurator(ConfigFile = "../../log4net.config", Watch = true)]

// Web程序：
[assembly: log4net.Config.XmlConfigurator(Watch = true)]

// 可在任意 namespace 上边声明，但是声明到 AssemblyInfo.cs 是全局都有效的。
```


4. 开始使用  
- (1)先在 class 中 using log4net;    
- (2)然后声明一个记录器变量：
``` csharp 代码说明 http://blog.ildh.net Liu Donghui's blog
private static ILog log = LogManager.GetLogger(MethodBase.GetCurrentMethod().DeclaringType);
或者
var ILog log = LogManager.GetLogger(给你的记录器起个名字);
```
- (3)使用  
``` csharp 
log.Info("这里写你的日志信息");// Info 代表日志等级  

//加了 Exception后，会在日志信息的最后，换行然后追加异常信息  
log.Error("日志信息",new Exception("这里是异常信息"));

// 日志等级有：ALL,FATAL,ERROR,WARN,DEBUG,INFO  
```
  
如果是记录到文本文件，那么按照本教程，就可以成功创建日志啦  
如果是写入到数据库，那么需要先建表，建表的语句在配置文件中已经写了，注意，如果表创建不正确，是写入不了数据库的  
（小哥哥被坑的快崩溃了才发现的）  
  
### 完成
好了，简单版教程就是这样了，基本使用是没有问题的，真正使用后你会发现日志的格式化可能不是你所满意的，所以后面小编会继续更新如何自定义日志模板  
如有不正确的地方，或者不清楚，可以与小编交流哦  

{% blockquote %}
**QQ：**3135366144
**Email：**ildgmsg@163.com
**微信：**iliudonghui
**微信公众号：**95qcs
{% endblockquote %}
共勉~

### 未完待续...