============
crondeamon
============
***************
1.介绍
***************
crondeamon是用来管理计划任务及后台任务的项目， 其功能相当于supervisor+crontab，  基于twisted   django 框架。  crondeamon集群有三个角色：

1.slave  slave主要是用来控制进程的启动和销毁

2.master master主要是集中控制所有的slave节点

3.ui     ui主要是提供web界面

***************
2.依赖
***************
python版本要求：

python>=2.6.x 

pip

mysql

***************
3.安装
***************
三台机器，192.168.8.94   192.168.8.95  192.168.8.96   系统环境：centos 6   python版本：2.7.10  ， 数据库：host = 192.168.15.34  port = 3306  user = zhou   password =zhou  database = crondeamon 

角色规划：

slave:192.168.8.94 192.168.8.94  192.168.8.96 

master:192.168.8.94 

ui: 192.168.8.94

slave安装：

192.168.8.94：
 ::

  [root@hadoop94 /]# pip install  git+git://github.com/zhoukunpeng504/crondeamon.git
  [root@hadoop94 /]# vim /etc/crondeamon/slave.ini                                                                                                          
  [crondeamon]
  host = 192.168.8.94
  mysqlhost = 192.168.15.34
  mysqlport = 3306
  mysqldb = crondeamon
  user = zhou
  passwd = zhou                                                                                                            
  charset = utf8

  [root@hadoop94 /]# python -m crondeamon.sbin.slave -c start
  /usr/local/lib/python2.7/site-packages/crondeamon/common/valid_mysql.py:112: Warning: Duplicate index 'owner_2' defined on the table 'crondeamon.cron_task'. This is deprecated and will be disallowed in a future release.
  cursor.execute(i)
  start success!
  [root@hadoop94 /]# ps aux|grep twistd
  root     31664  0.0  0.3 475548 20116 ?        Sl   09:56   0:00 /usr/local/bin/python2.7 /usr/local/bin/twistd --pidfile /data/crondeamon/slave/pid/crondeamon-slave.pid --logfile /data/crondeamon/slave/log/crondeamon-slave.log crondeamon-slave
  root     31697  0.0  0.0 103248   892 pts/0    S+   09:56   0:00 grep twistd
end





