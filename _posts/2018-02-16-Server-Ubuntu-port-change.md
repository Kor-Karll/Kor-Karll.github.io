---
layout: post
title: "[Server] DB/FTP/SSH 포트변경"
category: Server
tags:
- 서버
- 포트변경
- Port
lastmod : 2018-02-16 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->

- FTP

```
vi /etc/vsftpd.conf

listen=NO 를

=> listen=YES

   listen_port = '원하는포트' 로 변경한다.
```

- DB (MariaDB)

```
vi /etc/mysql/mariadb.conf.d/50-server.cnf

[mysqld]

port = 3306 을

=> port = '원하는 포트' 로 변경한다.
```

- ssh

```
vi /etc/ssh/sshd_config

Port = 21 를 변경한다.
```

- Service 부분

```
vi /etc/services

ftp-data     21/tcp

ftp           21/udp

ssh         22/tcp

ssh         22/udp

mysql       3306/tcp

mysql       3306/udp

을 변경한다.
```