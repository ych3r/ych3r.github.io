---
title: 端口 & 服务
categories:
 - methodology
tags:
 - info gathering
 - cheatsheet
---

# 文件共享服务端口

端口 | 服务 | 利用
---|---|---
21/22/69 | FTP/TFTP | 允许匿名上传、下载、破解和嗅探
2049 | NFS | 配置不当
139 | Samba | 破解、未授权访问、RCE
389 | LDAP | 注入、允许匿名访问、弱口令

# 远程连接服务端口

端口 | 服务 | 利用
---|---|---
22 | SSH | 破解、SSH 隧道及内网代理转发、文件传输
23 | Telnet | 破解、嗅探、弱口令
3389 | RDP | Shift 后门、破解
5900 | VNC | 弱口令
5632 | PyAnywhere | 抓密码、代码执行

# Web 应用服务端口

端口 | 服务 | 利用
---|---|---
80/443/8080 | 常见 Web 端口 | Web 攻击、破解、服务器版本漏洞
7001/7002 | WebLogic 控制台 | Java 反序列化、弱口令
8080/8089 | Jboss/Resin/Jetty/Jenkins | 反序列化、控制台弱口令
9090 | WebSphere 控制台 | Java 反序列化、弱口令
4848 | GlassFish 控制台 | 弱口令
1352 | Lotus Domino 邮件服务 | 弱口令、信息泄漏、破解
10000 | Webmin-Web 控制面板 | 弱口令

# 数据库服务端口

端口 | 服务 | 利用
---|---|---
3306 | MySQL | 注入、提权、破解
1433 | MSSQL | 注入、提权、SA 弱口令、破解
1521 | Oracle | TNS 破解、注入、反弹 shell
5432 | PostgreSQL | 破解、注入、弱口令
27017/27018 | MongoDB | 破解、未授权访问
6379 | Redis | 可尝试未授权访问、弱口令破解
5000 | SysBase/DB2 | 破解、注入

# 邮件服务端口

端口 | 服务 | 利用
---|---|---
25 | SMTP | 邮件伪造
110 | POP3 | 破解、嗅探
143 | IMAP | 破解

# 网络常见协议端口

端口 | 服务 | 利用
---|---|---
53 | DNS | 允许区域传送、DNS 劫持、缓存投毒、欺骗
67/68 | DHCP | 劫持、欺骗
161 | SNMP | 破解、搜集目标内网信息

# 特殊服务端口

端口 | 服务 | 利用
---|---|---
2181 | Zookeeper | 未授权访问
8069 | Zabbix | RCE、SQL 注入
9200/9300 | Elasticsearch | RCE
11211 | Memcache | 未授权访问
512/513/514 | Linux Rexec | 破解、Rlogin 登录
873 | Rsync | 匿名访问、文件上传
3690 | SVN | SVN 泄露、未授权访问
50000 | SAP Management Console | RCE

---
ref:
[《Python 安全攻防——渗透测试实战指南》](https://my.oschina.net/u/4583000?q=python)