---
layout: post
title: "[Server] DB Warning 메세지"
category: Server
tags:
- Server
- MySQL
- MariaDB
- Warning
- Error Massage
lastmod : 2018-02-18 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

세팅한 서버에 워닝이 자꾸 뜬다고 하여 /etc/messages 를 확인하여 보았다.

```
 mysqld: 2016-09-20  9:46:34 [Warning] IP address '111.111.111.111' could not be resolved: Name or service not known
```

위와 같은 경고 메세지가 확인돼었다.

<!--미리보기-->

찾아보니 mysql에 접속할때 ip정보를 hostname으로 변환해주는 dns 작업을 하는데 이것을 설정하지 않아 생기는 오류라 한다.

원문 :

---

간혹 DB 서버가 아래 첨부된 내용과 같은 로그를 발생 하며 비정상적인 종료가 발생 할 경우가 있습니다.

```
2015-09-03 17:38:03 14527 [Warning] IP address '1.215.' could not be resolved: Name or service not known
2015-09-03 19:26:52 14527 [Warning] IP address '117.21' could not be resolved: Name or service not known
2015-09-03 20:22:52 14527 [Warning] IP address '221.' could not be resolved: Name or service not known
2015-09-04 06:08:55 14527 [Warning] IP address '61.' could not be resolved: Name or service not known
2015-09-04 09:25:35 14527 [Warning] IP address '223.' could not be resolved: Temporary failure in name resolution
2015-09-04 09:25:36 14527 [Warning] IP address '223.' could not be resolved: Temporary failure in name resolution
2015-09-04 10:38:38 14527 [Warning] IP address '222.' could not be resolved: Name or service not known
2015-09-04 12:31:46 14527 [Note] /usr/local/mysql/bin/mysqld: Normal shutdown
2015-09-04 12:31:48 14527 [Warning] /usr/local/mysql/bin/mysqld: Forcing close of thread 4  user: 'root'
```

mysql 서버에 접속 할 경우 IP정보를 hostname으로 변환 해주는 DNS질의를 진행 합니다.

이때 /etc/resolv.conf에 설정된 DNS정보가 올바르게 설정 되지 않아, 접속 지연 현상이 발생 하며, 간혹 첨부된 로그와 같이 mysqld이 종료 되는 현상이 발새 합니다.

이런 경우 아래와 같은 설정으로 해당 문제를 해결 할수있습니다.

1. my.cnf 파일에 추가 
- skip-name-resolve

2. mysqld 데몬 재구동
- /usr/local/mysql/bin/mysqld_safe restart

3. 설정 조회
```
mysql> SHOW VARIABLES LIKE 'skip_name_resolve';
+-------------------+-------+ 
| skip_name_resolve | ON    | 
+-------------------+-------+
```
---

참고 : 

[http://faq.hostway.co.kr/Linux_DB/8176](http://faq.hostway.co.kr/Linux_DB/8176)

[http://codeinthehole.com/writing/solving-mysql-connection-problems-caused-by-a-dead-name-server/](http://codeinthehole.com/writing/solving-mysql-connection-problems-caused-by-a-dead-name-server/)

[https://bugs.mysql.com/bug.php?id=35777](https://bugs.mysql.com/bug.php?id=35777)