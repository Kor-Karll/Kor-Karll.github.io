---
layout: post
title: "[DB] MariaDB mysqldump 활용"
category: DB
tags:
- MariaDB
- MySQL
- 백업
lastmod : 2018-03-12 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

mysqldump 는 SQL 포멧의 텍스트로 백업 생성

<!--미리보기-->

### 형식

```
mysqldump --user=backupuser -p --all-databases > backup.sql
```

- 정상적으로 수행되고 나면 

```
Dump completed on <date> <time>
```

- 실패한다면 에러 메시지 출력됨


### 옵션

- --add-drop-databse : 데이터베이스를 삭제한 후 데이터를 복원전 생성하는 커맨드 추가

- --add-drop-table : 위와 마찬가지로 테이블 재생성

- --add-locks : 테이블 앞과 뒤에 LOCK TABLES 와 UNLOCK TABLES 커맨드를 추가한다. 테이블을 락시키면 복원속도가 빨라진다
