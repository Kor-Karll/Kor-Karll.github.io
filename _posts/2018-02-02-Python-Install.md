---
layout: post
title: "[Python] 파이썬 최신버전 설치하기(CentOS)"
category: Python
tags:
- Python
- Install
- Latest Version
lastmod : 2018-02-02 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

<a href="https://www.python.org/downloads/">https://www.python.org/downloads/</a>

해당 경로로 들어간후 "Python-3.X.X.tgz" 를 다운로드한다.

<!--미리보기-->

1. 다운로드한 파일의 압축을 푼다

```
$ tar xvzf Python-3.6.3.tgz
```

2. 해당 디렉터리로 이동

```
$ cd Python-3.6.3
```

3. Makefile 파일을 만들기 위해서 configure를 실행한다.

```
$ ./configure
```

4. 파이썬 소스를 컴파일

```
$ make
```

5. 설치

```
$ make install
```

출처 : <a href="https://wikidocs.net/8">Link</a>



***