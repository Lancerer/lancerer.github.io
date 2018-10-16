---

layout:post
title:"markdown的使用"
date:2018-10-16 16:31
categories: markdown
tags: markdown jshint csslint
---
* content
{:toc}

本文我将讲述一下 SublimeLinter 的安装过程。其组件 jshint 的安装与使用。其组件 csslint 的安装与使用。我将基于 [Sublime Text 3](http://sublimetext.com/3) 来安装。使用 Sublime Text 2 的用户阅读本文是没有帮助的。

SublimeLinter 是 Sublime 的插件，它的作用是检查代码语法是否有错误，并提示。习惯了 IDE 下写代码的人一定需要一款在 Sublime 上类似的语法检查工具。下面我们开始。

## 安装 SublimeLinter   

如同其他插件一样使用 Package Control 来安装。   

1. 按下 `Ctrl+Shift+p` 进入 Command Palette   
2. 输入`install`进入 Package Control: Install Package   
3. 输入`SublimeLinter`。进行安装.   

![SublimeLinter](http://7q5cdt.com1.z0.glb.clouddn.com/SublimeLinter-sublimeLinter.jpg)   

安装完成后可以看到这样一段话：   

```
Welcome to SublimeLinter, a linter framework for Sublime Text 3.

                  * * * IMPORTANT! * * *

         SublimeLinter 3 is NOT a drop-in replacement for
        earlier versions.

         Linters *NOT* included with SublimeLinter 3,
         they must be installed separately.

         The settings are different.

                 * * * READ THE DOCS! * * *

 Otherwise you will never know how to install linters, nor will
 you know about all of the great new features in SublimeLinter 3.

 For complete documentation on how to install and use SublimeLinter,
 please see:

 http://www.sublimelinter.com
```
