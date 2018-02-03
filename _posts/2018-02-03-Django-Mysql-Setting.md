---
layout: post
title: Django mariadb 설정(CentOS)
tags:
- Django
- MariaDB
- 설정
- CentOS
lastmod : 2018-02-03 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---
서버(CentOS)에 Django를 설치한후 MariaDB를 설정
<!--미리보기-->
***

PyMySQL 설치

```
pip3 install PyMySQL
```

프로젝트명\settings.py 편집

``` python
import pymysql
pymysql.install_as_MySQLdb()

DATABASES = {
    'default': {
            'ENGINE': 'django.db.backends.mysql',
            'NAME'          : '데이터베이스명',
            'USER'          : '접속유저',
            'PASSWORD'      : '비밀번호',
            'HOST'          : 'localhost',
            'PORT'          : '포트번호',
    }
}
```



