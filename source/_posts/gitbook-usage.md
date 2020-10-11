---
title: 初识gitbook 
date: 2020-10-10 17:37:38
tags: 
	- gitbook
	- 工具
	- tool
categories:
	- 写作
---

## {% span blue, 背景 %}
为了在实验上深耕下去，正在阅读一本英文版的实验书籍，突然有了翻译成中文版的想法，调研了下写书工具，发现gitbook是不错的选择，可以使用markdown，还有git进行版本管理，逼格满满。

## {% span blue, 安装 %}
由于gitbook基于node.js，首先需要保证你的机器上已安装好node，不属于主要内容，就不做介绍了。

然后开始安装gitbook，输入以下命令进行安装：
{% codeblock %}
$ npm install -g gitbook-cli
{% endcodeblock %}
安装完成后，通过下列命令验证是否安装成功：
{% codeblock %}
$ gitbook -V
CLI version: 2.3.2
GitBook version: 3.0.0
{% endcodeblock %}
更多命令参看 {% link GitBook 安装文档, https://github.com/GitbookIO/gitbook/blob/master/docs/setup.md %}
<!-- more -->
## {% span blue,  开始写书 %}
创建并进入你要写书的目录，调用下面的命令：
{% codeblock %}
$ gitbook init
warn: no summary file in this book
info: create README.md
info: create SUMMARY.md
info: initialization is finished
{% endcodeblock %}
命令输出可以看出，命令执行后创建了两个文件README.md和SUMMARY.md，其中SUMMARY.md记录的是书的章节目录，添加几个章节：
{% codeblock %}
# Summary

* [前言](preface.md)
* [Part I 入门主题](PartI/preface.md)
	* [1.概述和实验动机](PartI/1.IntroductionAndMotivation/preface.md)
{% endcodeblock %}
同时根据SUMMARY.md列出的文件创建出来：
{% codeblock %}
$ tree
.
├── PartI
│   ├── 1.IntroductionAndMotivation
│   │   └── preface.md
│   └── preface.md
├── README.md
├── SUMMARY.md
└── preface.md
{% endcodeblock %}
现在就可以尝试看看效果了，运行如下命令：
{% codeblock %}
$ gitbook serve
Live reload server started on port: 35729
Press CTRL+C to quit ...

info: 7 plugins are installed
info: loading plugin "livereload"... OK
info: loading plugin "highlight"... OK
info: loading plugin "search"... OK
info: loading plugin "lunr"... OK
info: loading plugin "sharing"... OK
info: loading plugin "fontsettings"... OK
info: loading plugin "theme-default"... OK
info: found 1 pages
info: found 1 asset files
info: >> generation finished with success in 0.5s !

Starting server ...
Serving book on http://localhost:4000
{% endcodeblock %}
使用浏览器输入 http://localhost:4000 ，可以看到图中内容：
{% image https://cdn.jsdelivr.net/gh/yfzhang-nk/cdn-assets@master/picture/gitbook_example.png, %}
自此gitbook可以投入使用了，可以开始写书了。

