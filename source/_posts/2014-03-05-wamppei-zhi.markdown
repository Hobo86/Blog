---
layout: post
title: "WAMP+ThinkPHP配置"
date: 2014-03-05 18:30
comments: true
categories:
- WAMP
- ThinkPHP
keywords: ThinkPHP,WAMP
description: ThinkPHP开发环境WAMP部署，.htaccess，自定义路径，自定义域名
---

配置ThinkPHP开发环境
</br>1、开启Rewrite支持.htaccess
</br>2、自定义工程路径
</br>3、自定义本地域名访问

WAMP安装
</br>http://www.wampserver.com/en/#download-wrapper

{% codeblock 编辑wamp/bin/apache/Apache2.x.x/conf/httpd.conf lang:ruby %}

#开启rewrite，支持.htaccess
#LoadModule rewrite_module modules/mod_rewrite.so去掉注释
LoadModule rewrite_module modules/mod_rewrite.so

#开启httpd-vhosts，自定义域名和工程路径
#Include conf/extra/httpd-vhosts.conf去掉注释
Include conf/extra/httpd-vhosts.conf

{% endcodeblock %}
<!--more--> 

自定义本地域名和工程路径
{% codeblock 编辑wamp/bin/apache/Apache2.x.x/conf/extra/httpd-vhosts.conf lang:ruby %}

#自定义工程路径
#d:projectpath工程路径
#mylocalhost.com自定义域名
#注意AllowOverride 是All，与wamp主界面不同
#可以定义其他端口
<VirtualHost *:80>  
  DocumentRoot d:projectpath 
  ServerName myhost.com 
  <Directory "d:projectpath"> 
      Options Indexes FollowSymLinks 
      AllowOverride All 
      Order allow,deny 
      Allow from all 
  </Directory> 
</VirtualHost>

#添加wamp主界面，假设wamp安装在D盘
<VirtualHost *:80>  
  DocumentRoot d:wamp/www 
  ServerName wamp.com 
  <Directory "d:wamp/www"> 
      Options Indexes FollowSymLinks 
      AllowOverride None 
      Order allow,deny 
      Allow from all 
  </Directory> 
</VirtualHost>

{% endcodeblock %}

去掉URL中的index.php
{% codeblock .htaccess lang:ruby %}

<IfModule mod_rewrite.c>
RewriteEngine on
RewriteCond %{SCRIPT_FILENAME} !-f
RewriteCond %{SCRIPT_FILENAME} !-d
RewriteRule ^(.*)$ index.php/$1 [QAS,PT,L]
</IfModule>

{% endcodeblock %}

{% codeblock 修改系统hosts lang:ruby %}

127.0.0.1 	myhost.com
127.0.0.1 	wamp.com

{% endcodeblock %}

重启Apache

查看成果吧
</br>myhost.com
</br>wamp.com



