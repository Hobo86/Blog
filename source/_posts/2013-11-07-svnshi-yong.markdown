---
layout: post
title: "SVN:使用"
date: 2013-11-07 18:15
comments: true
categories: 
- SVN
keywords: SVN, 配置, 自动部署
description: Centos 安装SVN，配置，自动部署等
---
1.系统
Centos 6.4 

2.安装svn
{% codeblock lang:ruby %}
#yum install subversion
{% endcodeblock %}
3.建立版本库
{% codeblock lang:ruby %}
#mkdir /mnt/svndata
{% endcodeblock %}
启动服务
{% codeblock lang:ruby %}
#svnserve -d -r /mnt/svndata
#svnadmin create /mnt/svndata/svn
{% endcodeblock %}
4.修改配置
{% codeblock lang:ruby %}
#cd /mnt/svndata/svn/conf
#vi svnserve.conf
anon-access=none
auth-access=write
password-db=passwd

#vi passwd
[users]
hobo=123456
{% endcodeblock %}
<!--more-->  
5.实现SVN与WEB同步

1)checkout一个test项目
{% codeblock lang:ruby %}
#svn co svn://localhost/svn /mnt/www/webroot/test
{% endcodeblock %}
2)修改权限为WEB用户
{% codeblock lang:ruby %}
#chown -R apache:apache /mnt/www/webroot/test
{% endcodeblock %}
3)建立同步脚本
{% codeblock lang:ruby %}
#cd /mnt/svndata/svn/hooks/
#cp post-commit.tmpl post-commit
{% endcodeblock %}
4)编辑post-commit，添加同步脚本
{% codeblock lang:ruby %}
#vi post-commit
export LANG=en_US.UTF-8
SVN=/usr/bin/svn
WEB_TEST=/mnt/www/webroot/test
$SVN update $WEB_TEST –username hobo –password 123456
chown -R apache:apache $WEB
{% endcodeblock %}
5)增加脚本执行权限
{% codeblock lang:ruby %}
#chmod +x post-commit
{% endcodeblock %}