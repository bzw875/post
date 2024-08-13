---
title: 网站打不开的问题排查经验
date: 2023-08-18 11:00:48
updated: 2023-08-18 11:00:48
tags: 运维
categories:
---

自从vps到期之后网站就打不开，正常启动，但是本地就是访问不了。

## 排查
ping 得通不，是不是不幸被墙了
服务启动正常吗
使用ip访问看看，是不是域名解析问题
查看服务监听的是哪个端口
是不是vps关闭了80端口

## 结果
是vps关闭了80端口，接下要做的是就是打开80端口了。但是不要关闭防火墙功能，这样不推荐。


## 打开80端口

方法一、编辑 ```etc/sysconfig/iptables```文件

```vi etc/sysconfig/iptables```

在最后面新加一行


```-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT```

重启 iptables 服务


```service iptables restart```

方法二、iptables 配置规则

```ptables -I INPUT -p tcp --dport 3030 -j ACCEPT```


```service iptables save```

重启 iptables 服务


```service iptables restart```