---
layout: post
title: "Centos VSFTP配置"
date: 2014-10-17 16:18
comments: true
categories: 
---

安装
{% codeblock lang:ruby %}
yum install vsftp
{% endcodeblock %}

配置
{% codeblock /etc/vsftpd/vsftpd.conf lang:ruby %}
关闭匿名登录
#anonymous_enable=NO

user_list中的说明是userlist_deny
#userlist_enable=NO

FTP root
#local_root=/mnt/ftp

{% endcodeblock %}

添加登录用户
{% codeblock lang:ruby %}
添加用户
#useradd Hobo
设置密码
#passwd Hobo
加入user_list
#echo Hobo >> /etc/vsftpd/user_list
{% endcodeblock %}

重启
{% codeblock lang:ruby %}
#service vsftpd restart
{% endcodeblock %}