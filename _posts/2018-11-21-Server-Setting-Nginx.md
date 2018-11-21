---
layout: post
title: "[Server]Nginx 최신버전 설치"
category: Server
tags:
- CentOS
- Nginx
lastmod : 2018-11-21 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->

/etc/yum.repos.d/nginx.repo

위 경로 파일을 아래와 같이 편집

```
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/OS/OSRELEASE/$basearch/
gpgcheck=0
enabled=1
```
OS <- 해당 경로에 OS 입력 (ex: rhel , centos)
OSRELEASE <- 해당 경로에 버전 입력 (ex: 6 , 7)

위와 같이 파일 생성 후 

```
yum update
yum install nginx
```

위와 같이 실행하여 nginx 설치

참고 : http://nginx.org/en/linux_packages.html