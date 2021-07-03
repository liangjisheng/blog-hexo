---
title: InnoDBFail
date: 2021-07-03 18:38:33
tags:
---

```shell
sudo systemctl restart mysql
```

使用上面命令重启 mysql 的时候失败，提示查看 journalctl -xe， 得到下面的报错

<!--more-->

```log
2021-07-02T02:41:52.406001Z 0 [ERROR] InnoDB: The innodb_system data file 'ibdata1' must be writable
2021-07-02T02:41:52.406012Z 0 [ERROR] InnoDB: The innodb_system data file 'ibdata1' must be writable
2021-07-02T02:41:52.406015Z 0 [ERROR] InnoDB: Plugin initialization aborted with error Generic error
2021-07-02T02:41:53.006814Z 0 [ERROR] Plugin 'InnoDB' init function returned error.
2021-07-02T02:41:53.006838Z 0 [ERROR] Plugin 'InnoDB' registration as a STORAGE ENGINE failed.
2021-07-02T02:41:53.006845Z 0 [ERROR] Failed to initialize builtin plugins.
2021-07-02T02:41:53.006850Z 0 [ERROR] Aborting
```

原因就是没有正常关闭mysqld服务的情况下，对数据库参数进行改变导致的。因此重启后的服务器不支持InnoDB引擎
处理方法是删除数据目录下的ib_logfile0和ib_logfile1文件

```shell
rm -rf ib_logfile*
```
