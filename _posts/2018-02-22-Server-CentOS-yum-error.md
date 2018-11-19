---
layout: post
title: yum repository가 꼬였을 경우 yum 초기화하기
`: Server
tags:
- CentOS
- yum
- yum초기화
lastmod : 2018-02-22 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

yum repository가 꼬였을 경우 yum 초기화하기
yum 명령어를 이용해서 어플리케이션을 설치하다보면 가끔 repository가 꼬여서 yum install 등 옵션이 먹히지 않게 됩니다. 저 같은 경우는 openstack repository를 설치하다가 이런 경우가 몇 번 있었는데요. 간단하게 해결할 수 있는 방법이 있어서 글을 적어봅니다.

<!--미리보기-->

# 1. /etc/yum.repos.d/ 이동해서 repository 지우기

```
# cd /etc/yum.repos.d/ //repository 저장 디렉토리로 이동 
# ls -al  // repository 확인
# rm -f 삭제할 repository  // base는 지우시면 안돼요. 지웠다가 낭패 봤어요...
# ls -al  // 확인
```
# 2. /var/cache/yum/에서 캐쉬디렉토리 삭제

```
# cd /var/cache/yum/
# ls -al // 캐쉬 디렉토리 확인
# rm -rf x86_64
```

# 3. headers, packages, metadata 삭제

```
# yum clean headers
# yum clean packages
# yum clean metadata
```

출처 : [http://junhyung2.blogspot.kr/2015/02/yum-repository-yum.html](http://junhyung2.blogspot.kr/2015/02/yum-repository-yum.html)