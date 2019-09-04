---
layout: post
title: "[Web] Nodejs 최신 버전 설치"
category: Server
tags:
- Server
- Web
- Nodejs

lastmod : 2019-09-04 15:00:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->
### 1. Yum Repository 추가
2019 09 04 시점
- Latest Release :

```linux
# yum install -y gcc-c++ make
# curl -sL https://rpm.nodesource.com/setup_12.x | sudo -E bash -
```

- Stable Release :

```linux
# yum install -y gcc-c++ make
# curl -sL https://rpm.nodesource.com/setup_10.x | sudo -E bash -
```

### 2. Install

```linux
# sudo yum install nodejs
```

### 3. Nodejs & NPM 버전 확인

```linux
# node -v 

v12.8.0

# npm -v 

6.10.2
```

참고 : [How To Install Latest Nodejs on CentOS/RHEL 7/6](https://tecadmin.net/install-latest-nodejs-and-npm-on-centos/)