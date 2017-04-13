<!--
author: jockchou
date: 2015-07-22
title: 在Nginx上运行GitBlog
tags: GitBlog
category: GitBlog
status: publish
summary: 如果你自己拥有服务器或者云平台提供的云主机，我推荐你使用Linux+[Nginx](http://nginx.org/)来运行GitBlog，如果你目前只有Apache环境也是可以的。
-->

如果你自己拥有服务器或者云平台提供的云主机，我推荐你使用Linux+[Nginx](http://nginx.org/)来运行GitBlog，如果你目前只有Apache环境也是可以的。

## 域名解析 ##
将你准备好的域名解析到你的主机IP，推荐使用[dnspod](https://www.dnspod.cn/)来管理和监控你的域名，具体的使用方法参考dnspod官方说明文档，非常简单。

## Nginx+PHP运行环境 ##

首先安装好你的Nginx和PHP环境，PHP版本要求5.3以上。如果你没有安装过，可Google搜索相关教程，也可以参照Nginx和PHP官方的文档。这是第一步，有一个正常的Nginx + PHP的运行环境。

## 配置Nginx ##

nginx可参考如下配置：


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

将以上配置中的server_name和root改成你自己的，fastcgi_pass配成你的CGI进程端口。

这里需要格外注意的是，如果gitblog不是部署在web服务的根目录下，应当对rewrite规则进行相应的修改。例如，当gitblog的首页部署在 http://XXX.net/BBB/CCC/DDD/EEE/ 下，则上述配置中的`location / {}`块应当修改为

```
location /BBB/CCC/DDD/EEE/ {
    if (!-e $request_filename) {
        rewrite ^\/BBB/CCC/DDD/EEE(.*)$ /BBB/CCC/DDD/EEE/index.php?$1 last;
        break;
    }
}
```

## 权限配置 ##

由于GitBlog的缓存机制需要写`app/cache`目录，必要时请查看并修改这个目录的权限，以确保你的PHP拥有写这个目录的权限。通常你只需要将此目录的所属者和组修改成CGI的运行账户。


## 运行 ##

以上配置好以后，启动你的Nginx和CGI服务，上传GitBlog源代码到网站目录，通过浏览器访问解析到本机的域名观察页面效果。如果页面没有正常显示，通过错误码来检查你的CGI和Nginx配置。
