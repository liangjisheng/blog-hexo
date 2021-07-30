---
title: sudo-su.md
date: 2021-07-19 21:00:21
tags:
---

## sudo, su, su -的区别

sudo是一种权限管理机制, 依赖于/etc/sudoers, 其定义了授权给哪个用户可以以管理员的身份能够执行什么样的管理命令
格式: sudo -u USERNAME COMMAND

<!--more-->

su为switch user, 即切换用户的简写, su是最简单的身份切换名, 用su我们能够进行不论什么用户的切换
一般都是su username, 然后输入password就ok了, 可是root用su切换到其它身份的时候是不须要输入password的
如果不指定USERNAME(用户名), 默认即为root

su -, su -l或su --login 命令改变身份时, 也同时变更工作目录, 以及HOME, SHELL, USER, LOGNAME
此外也会变更PATH变量. 用su -命令则默认转换成成root用户了
而不带参数的"su命令"不会改变当前工作目录以及HOME,SHELL,USER,LOGNAME. 只是拥有了root的权限而已

sudo 命令需要输入当前用户的密码, su 命令需要输入 root 用户的密码
鉴于 sudo 命令要求输入的是其他用户自己的密码, 所以不需要共享 root 密码
同时想要阻止特定用户访问 root 权限, 只需要调整 sudoers 文件中的相应配置即可

sudo 命令只允许使用提升的权限运行单个命令, 而 su 命令会启动一个新的 shell
同时允许使用 root 权限运行尽可能多的命令, 直到明确退出登录
