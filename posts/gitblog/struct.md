<!--
author: jockchou
date: 2015-07-29
title: GitBlog目录结构
tags: GitBlog
category: GitBlog
status: publish
summary: GitBlog采用流行的PHP框架CodeIgniter开发，只是我对一些目录进行了重命名。如果你熟悉CodeIgniter框架，那你一定不会陌生。
-->
GitBlog采用流行的PHP框架`CodeIgniter`开发，只是我对一些目录进行了重命名。如果你熟悉CodeIgniter框架，那你一定不会陌生。

## 目录结构如下 ##

GitBlog的目录结构如下所示：


```
.
├── app
│   ├── cache
│   └── logs
├── theme
│   ├── default
│   ├── quest
│   └── simple
├── sys
├── img
├── posts
├── conf.yaml
├── favicon.ico
├── index.php
├── LICENSE
└── robots.txt
```
## 2.2版本变化 ##
从2.2版本开始，img和posts目录已经统一到blog目录。
2.2之前的版本图片和markdown文件是分别放在img和posts目录，这样不太方便管理和备份。
这个版本，我们统一放在blog目录中，图片推荐放在blog/img目录中，在markdown中使用相对路径引用图片。
如果你不想修改以前markdown中的路径，你仍然可以使用根目录下的img文件夹中的图片，只是我们推荐以后的图片都放到blog目录中与markdown文件一起管理。 

2.2以后的目录会是这样：

```
.
├── app
│   ├── cache
│   └── logs
├── theme
│   ├── default
│   ├── quest
│   └── simple
├── sys
├── blog
│   └── img
├── conf.yaml
├── favicon.ico
├── index.php
├── LICENSE
└── robots.txt
```

## 目录说明 ##

- app: CodeIgniter主程序目录，cache和logs分别是缓存和日志目录，请确保写的权限    
- sys： CodeIgniter系统源码目录，一般不需要改这里面的任何东西  
- theme： GitBlog主题目录，所有主题模板都放在这里    
- posts: GitBlog存放markdown博客文件的目录，你写的博客都放这里  
- img： 图片目录，你的markdown中引用的图片都放到这里，使用相对路径引用  
- conf.yaml: GitBlog配置文件  
- index.php: 入口php文件  

注意：2.2版本开始统一将markdown文件和图片文件放到blog目录中。
 
