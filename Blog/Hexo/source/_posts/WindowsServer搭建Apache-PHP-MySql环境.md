---
title: WindowsServer搭建Apache+PHP+MySql环境
comments: true
categories:
  - 服务器
tags:
  - Apache
  - PHP
  - MySql
  - Windows
  - Windows Server
date: 2018-06-24 22:14:14
updated:
---
总结下市场主流的Apache+PHP+MySql环境的搭建。

<!-- more -->
# Windows 搭建 Apache + PHP + MySql 环境

# 简易四步走

## 准备
* 下载 PHP 
* 下载 Apache
* 下载 MySql

## 第一步：安装 PHP
1. 安装 PHP 。解压 PHP 至你想安装到的目录，比如 `D:/dev/php/`
2. 配置环境变量。将 `D:/dev/php/ext` 追加到 path 最后。（如果 path 编辑时只有1行，那就需要在前边增加分号 `;` ） 

## 第二步：安装 MySql
1. 安装 MySql。这个简单，百度一大堆。 `Mysql` 的默认安装路径是 `C:/Program Files/MySQL/MySQL Server 具体版本号/` 
2. 配置环境变量。新建系统环境变量 `MYSQL_HOME`，值为 `MySql` 的安装目录。将 `%MYSQL_HOME%\bin` 追加到 path  
（如果 path 编辑时只有1行，那就需要在前边增加分号 `;` ） 

## 第三步：配置 PHP
1. 将 php 安装目录下的 `pho.ini-develop` 文件备份，然后重命名为 `php.ini` ，打开进行编辑。
2. 去掉以下配置前面的分号
```
;extension_dir = "ext"  
;extension=php_gd2.dll  
;extension=php_mysql.dll  
;extension=php_mysqli.dll  
;extension=php_openssl.dll  
;extension=php_sockets.dll  

您的PHP环境不支持PDO, 但支持 mysql_connect, 这样系统虽然可以运行, 但还是建议你开启PDO以提升程序性能和系统稳定性  
;extension=php_pdo_mysql.dll
;extension=php_curl.dll
```
3. 完成

## 第四步：配置 Apache
1. 打开 Apache 的安装目录，找到 conf\httpd.conf，打开编辑。
2. 修改以下配置
```
Define SRVROOT "Apache 的安装目录"  
SRVROOT "Apache 的安装目录"  
DocumentRoot "Apache安装目录/htdocs" （这个是 PHP 和 HTML 存放的地方）
Listen 80 若80端口被占用，可以修改为其他端口
```
3. 然后在文件的末尾添加对PHP的支持
```
# php5 support 
LoadModule php5_module PHP安装目录/php5apache2_4.dll
AddType application/x-httpd-php .php .html .htm
# configure the path to php.ini
PHPIniDir "PHP安装目录"

# PHP7的话就换成这个

# php7 support
LoadModule php7_module PHP安装目录/php7apache2_4.dll
AddType application/x-httpd-php .php .html .htm
# configure the path to php.ini
PHPIniDir "PHP安装目录"
```
4. 安装 Apache 到 Windows 服务。  
以管理员身份运行命令行（shell），cd 命令一直找到 `Apache安装目录\bin` ，输入命令 `httpd -k install` ，完成安装。


## 可能遇到的情况
### 安装 Apache 服务，输入指令 `httpd -k install` 报如下错  
`无法启动此程序,因为计算机中丢失VCRUNTIME140.dll尝试重新安装此程序以解决此问题`  
这是因为缺少了`Microsoft.Net.Framework`的安装,  
(1)去微软官网下载 `Microsoft.Net.Framework 4.6.1`  ，适用于：  
`Windows 7 SP1` `Windows 8` `Windows 8.1` `Windows 10` `Windows Server 2008 R2 SP1` `Windows Server 2012` `Windows Server 2012 R2`  
[点击跳转下载地址](https://www.microsoft.com/zh-CN/download/details.aspx?id=49981)  
(2)去微软官网下载Visual C++ Redistributable for Visual Studio 2015  
[点击跳转下载地址](https://www.microsoft.com/zh-cn/download/details.aspx?id=48145)  
备注：如果服务器所在的windows操作系统是32位的，就下载vc_redist.x86.exe；如果是64位的，vc_redist.x64.exe与vc_redist.x86.exe最好都下载安装
注意点：vc_redist.x64.exe与vc_redist.x86.exe所属VC++版本需保持一直，比如都是2015或都是2012。

### 输入指令 `httpd -k install` 安装 Apache服务后，提示如下错  
`httpd.conf Cannot load php安装目录/php5apache2_4.dll`  
两种情况，第一种是缺少 `msvcr110.dll`，下载安装就好了。  
[点击跳转下载地址](http://www.microsoft.com/zh-CN/download/details.aspx?id=30679)  
选择下载 `VSU4\vcredist_x86.exe`，如果仍然不行，就换 `VSU4\vcredist_x64.exe`，我就是下的 x86 无效，更换为 x64 生效了  

### 安装 Apache 出现 `<OS 10013> 以一种访问权限不允许的方式做了一个访问套接字的尝试`  
这个问题是指80端口被占用了（查看端口使用情况：打开命令行CMD，输入 `netstat -a` 即可查看）  
修改 Apache安装目录/conf/httpd.conf  
将 `Listen 80` 更改为 `Listen 其他端口`

### 安装完环境后，打开网站没有启动 index.php 页面，在此节点后增加 index.php  
```bash 
<IfModule dir_module>
    DirectoryIndex index.html index.htm index.php
</IfModule>
```

### php 不支持 curl 的终极解决方案  
(1)取消注释  `extension=php_curl.dll`  
(2)设置 extension_dir，比如我的 php 放在 E 盘，就是 `extension_dir = "E:/php-5.6.30-x64/ext"` ,注意不能用"ext"，一定要写完整路径，否则找不到（我试了n多次，才发现这个问题）  
(3)复制php目录下 `libeay32.dll` , `libssh2.dll`, `ssleay32.dll` 到 apache 的 `bin` 下，比如我的 `E:\Apache24\bin`  
不需要放到 `windows\system32` 。

### windows 2008 r2 系统默认80端口被系统占用的处理 （更改这个80端口，浪费了好多时间，网上一堆教程都没用真是急人）
使用netstat 命令查看指定端口  
```bash
netstat -ano | findstr :80  
```
----如下所示：本地的80端口被进程为4的占用  
 ```bash
 TCP    0.0.0.0:80             0.0.0.0:0              LISTENING       4  
 TCP    192.168.1.207:60652    221.233.41.28:80       CLOSE_WAIT      17160  
 TCP    [::]:80                [::]:0                 LISTENING       4  
```
----任务管理器查看进 pid 为4
```bash
 进程名   pid  描述
 system   4    net kernel&System
```
 ----打开注册表，`Win+R` 运行 `regedit`
 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HTTP`  
 右边有一个'start'，右键修改它的`DWORD`值改为'4'。
 ----重启服务器后正常