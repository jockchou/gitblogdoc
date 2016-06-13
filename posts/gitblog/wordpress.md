<!--
author: jockchou
date: 2015-07-17
title: 从wordpress导入
tags: GitBlog
category: GitBlog
status: publish
summary: Gitblog从2.1版本开始支持从wordpress导入到Gitblog的功能，方便wordpress使用者快速转移博客到Gitblog。
-->

Gitblog从2.1版本开始支持从wordpress导入到Gitblog的功能，方便wordpress使用者快速转移博客到Gitblog。

## 从wordpress导出xml ##

第一步是要从wordpress管理后台使用自带工具导出wordpress.xml。worldpress管理后台，工具-》导出，选择文章项，下载导出的文件。

![wordpress.xml](http://pingodata.qiniudn.com/wordpress2gitblog.png)

将下载下来的xml文件重命名为`wordpress.xml`并复制到Gitblog根目录。

## 执行导入命令 ##

```
php /data/vhosts/jockchou.gitblog.cn/index.php wp2gb
```

也就是执行gitblog的wp2gb函数，成功后，会在`posts/wp`目录下生成导入的博客文件。










