---
title: 2016-12-1nodeJs sublime text3 开发环境搭建
layout: post
categories: document
tag: 学习笔记
---
 前言
============
原来一直想学习一下传说中的nodejs，今天终于算开了个章，把开发环境搭建好，下面记录搭建开发环境中的一些问题。
我搭建的环境实在sublime text 3中使用的，因为原来编写前台代码的时候一直使用sublime text 3对这款编辑器也有了自己的一些了解。（ps，我的快捷键一直用的是原来eclipse的快捷键 哈哈）

一、安装nodejs 插件
===================
我开始的时候是通过ppackage control安装的，但后面再bulid的时候出现了中文编码的问题，我一时没有找到解决方案，后面在网上搜到相对应解决方案，在github上面下载该项目的zip包 然后自己复制到sublime text的packpage 下 nodejs 插件的github地址[https://github.com/tanepiper/SublimeText-Nodejs ](https://github.com/tanepiper/SublimeText-Nodejs) ，关于自己packpage文件夹sublime text 3的preferences 下面的browser package点击就能打开相对应的文件，一般这个目录在c盘的user 下面 有一级目录会被隐藏，应该打开隐藏目录课件。
二、修改插件的配置文件
===============
Nodejs.sublime-settings 这个文件是设置相对应的nodeJS的安装目录的配置成下面

```
{
  // save before running commands
  "save_first": true,
  // if present, use this command instead of plain "node"
  // e.g. "/usr/bin/node" or "C:\bin\node.exe"
  "node_command": "C:/Program Files (x86)/nodejs/node.exe",
  // Same for NPM command
  "npm_command":"C:/Program Files (x86)/nodejs/npm.cmd",
  // as 'NODE_PATH' environment variable for node runtime
  "node_path": false,

  "expert_mode": false,

  "ouput_to_new_tab": false,
 
}

```
这里只是改动了node_command npm_command两个配置 只是将这两个配置改成自己的node目录以及npm目录

Nodejs.sublime-bulid文件就相对复杂一些

```
{
  "cmd": ["node", "$file"],
  "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
  "selector": "source.js",
  "shell":true,
  "encoding": "utf8",
  "windows":
    {
		// 1      "cmd": ["taskkill /F /IM node.exe & node", "$file"]

	//	 2 "cmd": ["node", "$file"]
         "cmd": ["nodemon", "$file"]
    },
  "linux":
    {
        "cmd": ["killall node; node $file"]
    },
    "osx":
    {
        "cmd": ["killall node; node $file"]
    }
}

```
有两种配置方式 一、windows{ 1 2}我注释掉的就是我开始的配置，表示 先把node进程结束掉 在启动node 执行当前文件，（ps 我开始的时候没有加上1 导致我每次Ctrl+B 的时候都报错 说node 端口已经背占了 每次只能够在cmd中 自己来结束进程）
配置方式二、第二种就是在安装了nodemon 之后，才可以配置的关于nodemon 自己搜，然后就不用每次修改之后从新Ctrl+b
他自动就重启了。


	




