<!--
author: jockchou
date: 2015-07-18
title: Gitblog升级
tags: GitBlog
category: GitBlog
status: publish
summary: 使用Gitblog老版本的用户可以在官网或者Gitbub上下载最新的Gitblog包进行升级，本文针对Gitblog升级的一些注意事项进行说明。
-->

使用Gitblog老版本的用户可以在官网或者Gitbub上下载最新的Gitblog包进行升级，本文针对Gitblog升级的一些注意事项进行说明。

## 备份 ##

在升级之前，请先备份好原来的Gitblog资源。这里包括所有的博客文件，即`posts`文件夹下面的所有markdown文件，这是最重要的，请务必备份好你的博客数据，以免错误操作导致博客丢失！以下列出了需要做好备份的内容：

- conf.yaml
- posts
- img

备份好你的配置文件，博客数据和相关的图片文件，以免丢失。


## 覆盖安装Gitblog ##

下载最新的Gitblog包，解压覆盖老的Gitblog目录，注意这时候你的配置文件也被覆盖了，你需要把之前的备份的配置文件再还原过来。



