<!--
author: jockchou
date: 2015-07-30
title: GitBlog安装
tags: GitBlog
category: GitBlog
status: publish
summary: 这是Giblog的一个简单安装教程，如果你熟悉PHP或Web开发，这对你来说一定非常简单。本教程只针对Linux+Nginx环境，对于使用Apache的用户请参考Apache配置章节。
-->

这是Giblog的一个简单安装教程，如果你熟悉PHP或Web开发，这对你来说一定非常简单。本教程只针对Linux+Nginx环境，对于使用Apache的用户请参考[在Apache上运行GitBlog](http://gitblogdoc.sinaapp.com/blog/gitblog/apache.html)。

## 环境准备: ##

- 域名
- Linux主机
- php + php-fpm
- nginx

假设我的域名为：
```
jockchou.gitblog.cn
```

## Linux主机 ##

如果你想自己购买主机搭建Gitblog，我推荐[阿里云][1]。我不得不承认这是一个广告链接，Gitblog作为一个开源软件，需要经济的支撑，如果你不需要云主机请忽略，如果你需要，感激你通过点击下面图片链接去购买，非常感激您的支持！

[![aliyun](../../img/640-90.gif)][1]

## 配置nginx虚拟主机 ##

假设我的nginx配置的网站根目录为：

```
/data/vhosts/jockchou.gitblog.cn
```

GitBlog采用[CodeIgniter](http://codeigniter.org.cn/)开发，nginx可参考如下配置：

```
server {
        listen       80;
        server_name  jockchou.gitblog.cn;
        root         /data/vhosts/jockchou.gitblog.cn;
        index        index.html index.htm index.php;

        location ~ \.(jpg|png|gif|js|css|swf|flv|ico)$ {
                 expires 12h;
        }

        location / {
                if (!-e $request_filename) {
					rewrite ^(.*)$ /index.php?$1 last ;
					break;
                }
        }

        location ~* ^/(doc|logs|app|sys)/ {
                return 403;
        }
    
        location ~ .*\.(php|php5)?$
        {
                fastcgi_connect_timeout 300;
                fastcgi_send_timeout 300;
                fastcgi_read_timeout 300;
                fastcgi_pass   127.0.0.1:9000;
                fastcgi_index  index.php;
                fastcgi_param  SCRIPT_FILENAME $document_root$fastcgi_script_name;
                include        fastcgi_params;
        }
}
```
在根目录下写一个`index.php`文件

```
<?php phpinfo();?>
```
启动nginx和php-fpm，在浏览器中访问域名`http://jockchou.gitblog.cn`正常显示phpinfo的内容表示安装环境成功了。

## 下载GitBlog源码包 ##

到[这里](https://github.com/jockchou/gitblog/releases)下载最新的GitBlog源码包，下传到你的服务器，解压复制包中的所有文件到网站根目录:
```
/data/vhosts/jockchou.gitblog.cn
```
再访问域名，就能看到GitBlog的默认页面了。

## 权限问题 ##

确保`blog`拥有读权限  
确保`app/cache`和`app/logs`目录的写权限  

假如运行php-fpm的用户名为apache：

```
chown -R apache:apache ./app/cache
chown -R apache:apache ./app/logs
```

## 其他需要注意的问题 ##

- 确保你已经安装了`mbstring`扩展库  
- 确保php.ini开启了short_open_tag = On  
- 确保php的版本在5.2.4以上  

[1]:http://s.click.taobao.com/t?e=m%3D2%26s%3DJAcK5vWm%2B5ccQipKwQzePCperVdZeJviEViQ0P1Vf2kguMN8XjClAjmpXs8CkRZL%2BxALKcubbqbv7wpOk8XUAdCkBxwNwRWDUeDgcRthI5AqjryzAeP7OzDVuRn8ddiDsEVVC24eqozcHtRpEUy6RHVyxRO0gvF4QxJtmCgOmCLXl8Q7TEjBF%2BX11FSyvDCnQiv%2BJKjlPObGDmntuH4VtA%3D%3D

