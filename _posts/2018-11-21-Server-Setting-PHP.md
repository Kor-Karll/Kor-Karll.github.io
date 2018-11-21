---
layout: post
title: "[Server] PHP,MariaDB 최신버전 설치"
category: Server
tags:
- CentOS
- PHP
- MariaDB
lastmod : 2018-11-21 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->
# PHP

remi repository를 yum 에 추가

```
$ wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
$ rpm -Uvh epel-release-latest-7.noarch.rpm
$ wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm
$ rpm -Uvh remi-release-7.rpm

$ yum install -y yum-utils
$ yum-config-manager --enable remi-php72

$ yum install php72
```

참고 : https://blog.asamaru.net/2018/02/14/install-php-7-2-on-centos-with-remi-rpm-repository/

# MariaDB

/etc/yum.repos.d/MariaDB.repo

위 경로 파일 설정

```
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.3.11/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```

위 파일 저장후

```
yum update
yum install MariaDB-server MariaDB-client
```


참고 : https://mariadb.com/kb/en/library/yum/
