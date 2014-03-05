---
layout: post
title: "MySQL:常用命令行"
date: 2013-10-30 08:58
comments: true
categories: 
- MySQL
keywords: MySQL, 权限, 导入, 导出, 命令
description: MySQL常用的命令行操作
---

登入
</br>mysql -h192.168.1.110  -uroot -ppassword
 
登出
</br>quit/exit
 
查看数据库
</br>show databases;
 
用户权限
</br>添加
</br>grant select on db.table to 'user'@'host';
</br>grant select,update on *.* to 'test'@'%';
</br>撤销
</br>revoke all on *.* from 'test'@'%';
</br>查看
</br>show grants;
</br>show grants for user@localhost
 
删除用户
</br>delete from mysql.user where user='' and host='';
 
设置密码
</br>update mysql.user set password=PASSWORD('123456') where user='root';
 
配置远程连接
</br>GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION; 
 
<!--more-->  

导出  
</br>mysqldump -u　用户名 -p 数据库名 > 数据库名.sql 
{% codeblock lang:ruby %} 
mysqldump -u　root -p dbname > filepath.sql  
#To export tofile(data only)
mysqldump -u [user]-p[pass]--no-create-db --no-create-info mydb > mydb.sql
#To export tofile(structure only)
mysqldump -u [user]-p[pass]--no-data mydb > mydb.sql
#To import todatabase
mysql -u [user]-p[pass] mydb < mydb.sql
{% endcodeblock %}
 
 
导入
{% codeblock lang:ruby %} 
mysql> use dbname             #切到要导入的数据库
mysql> source filepath.sql
{% endcodeblock %}
 
变量查看/修改
{% codeblock lang:ruby %} 
show variables like '%slow%';
set global slow_query_log= 'ON';

show status like 'Qca%';
 
#查看SQL中select条数
show status like 'Com_sel%'; #显示的是一次会话的值！
show global status like "Com_select";
{% endcodeblock %}
 
找回密码？
</br>1、kill -TERM mysqld
</br>2、conf中加入skip-grant-tables
</br>3、service mysqld restart
</br>4、mysql -uroot -p
</br>5、修改密码
</br>6、改回原配置并重启
 
Binlog：http://dev.mysql.com/doc/refman/5.7/en/mysqlbinlog.html
</br>删除mysql-bin日志
</br>http://dev.mysql.com/doc/refman/5.7/en/purge-binary-logs.html
</br>PURGE BINARY LOGS TO 'mysql-bin.010';
</br>PURGE BINARY LOGS BEFORE '2008-04-02 22:46:26';
 
清空表并使自增归0
</br>TRUNCATE TABLE tablename
 
Mac无法登陆
</br>Can't connect to MySQL server on '127.0.0.1' (61)
</br>StevenMacBookAir:~ Hobo$ sudo su -
</br>StevenMacBookAir:~ root# nohup /usr/local/mysql/bin/mysqld_safe &
</br>[1] 464
</br>StevenMacBookAir:~ root# appending output to nohup.out
</br>exit
</br>logout
</br>StevenMacBookAir:~ Hobo$ 

