---
layout: post
title: jekyll Windows下安装
date: 2015-05-05 16:05:39
category: "tools"
---

###安装 Ruby
前往 http://rubyinstaller.org/downloads/

在 “RubyInstallers” 部分，选择某个版本点击下载。
例如， Ruby 2.0.0-p451 (x64) 是适于64位 Windows 机器上的 Ruby 2.0.0 x64 安装包。

通过安装包安装.
(可能国内下载很么，需要通过翻墙)

###安装 DevKit

DevKit 是一个在 Windows 上帮助简化安装及使用 Ruby C/C++ 扩展如 RDiscount 和 RedCloth 的工具箱。 详细的安装指南可以在程序的wiki 页面 阅读。

再次前往 http://rubyinstaller.org/downloads/

下载同系统及 Ruby 版本相对应的 DevKit 安装包。 例如，DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe 适用于64位 Windows 系统上的 Ruby 2.0.0 x64。

下面列出了如何选择正确的 DevKit 版本：

Ruby 1.8.6 to 1.9.3: DevKit tdm-32-4.5.2
Ruby 2.0.0: DevKit mingw64-32-4.7.2
Ruby 2.0.0 x64: DevKit mingw64-64-4.7.2

运行安装包并解压缩至某文件夹，如 C:\DevKit

通过初始化来创建 config.yml 文件。在命令行窗口内，输入下列命令：

cd “C:\DevKit”
ruby dk.rb init
notepad config.yml

在打开的记事本窗口中，于末尾添加新的一行 - C:\Ruby200-x64，保存文件并退出。

回到命令行窗口内，审查（非必须）并安装。

ruby dk.rb review
ruby dk.rb install

###安装 Jekyll
国内需要VPN翻墙，否则基本上安装失败，使用淘宝替换sources
    gem sources --remove https://rubygems.org/
	gem sources -a http://ruby.taobao.org/
	gem sources -l
	CURRENT SOURCES ***
	http://ruby.taobao.org
	`#请确保只有 ruby.taobao.org`
	gem install rails
	
确保 gem 已经正确安装
	gem -v

输出示例：
	2.0.14

###安装 Jekyll gem

	gem install jekyll

###Jekyll 操作
在项目目录下执行命令部署，生产_site文件本地允许：
	jekyll serve