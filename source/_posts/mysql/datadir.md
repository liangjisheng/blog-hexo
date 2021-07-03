---
title: move mysql datadir
date: 2021-07-03 18:43:04
tags:
---

在16.04和18.04版本的mysql数据库，默认是5.7版本的，想要修改数据目录，需要修改2个地方
一个是mysql的配置文件，另一个是apparmor。
apparnor 是控制访问权限的， mysql依赖它

### 创建新的目录

```shell
mkdir /data/mysql
sudo chmod 0700 /data/mysql
sudo chown mysql:mysql /data/mysql
```

<!--more-->

### 移动数据

```shell
mv /var/lib/mysql/* /data/mysql
```

### 删除日志

> 不删除会报错

```shell
rm -rf /data/mysql/ib_logfile*
```

### 修改mysql配置文件

```shell
vim /etc/mysql/my.cnf
datadir=/data/mysql
```

### 修改apparmor的配置文件use.sbin.mysqld

```shell
vim /etc/apparmor/usr.sbin.mysqld
```

把

```txt
/var/lib/mysql/ r,  
/var/lib/mysql/** rwk,
```

修改为

```txt
/database/mysql/ r,  
/database/mysql/** rwk,
```

### 重启 apparmor

```shell
systemctl restart apparmor
```

### 重启 mysql

```shell
systemctl restart mysql
```

> 如果出现启动成功，但是测试新建数据库还是在原来的目录，试试重启服务器，或者仔细查看mysql配置文件，提醒一下 并不需要更改/usr/share/mysql/mysql-systemd-start 脚本中的datadir变量
