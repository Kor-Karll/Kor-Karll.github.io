---
layout: post
title: "[MySQL] 운영 관리 및 최적화"
`: DB
tags:
- MySQL
- 튜닝
- 인덱스
- 통계
lastmod : 2018-03-14 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->

- 테이블 상 PK를 지정하지 않더라도 내부적으로 임의의 PK를 만들어 저장함

### index 관리

- 통계 활성화

```
vi /etc/my.cnf.d/server.cnf

[mysqld]
userstat = 1
```

- 통계 정보가 충분히 모였다고 생각했을때 인덱스 통계를 출력

```
SHOW INDEX_STATISTICS;
```

- 통계를 바탕으로 인덱스 관리

---

### JOIN

![SQL JOIN]({{ site.baseurl }}/images/posts/2018-03-14-DB-MySQL-index-count-analytics/1.png)

---

### DATETIME 칼럼 마이크로초 단위 사용

- 사용자들은 애플리케이션의 응답 시간이 1초보다 짧길 기대, 해당 시간 추적을 위해 마이크로초 단위 사용
- datetime 형식의 칼럼은 디폴트 값 1초 단위이다
- 마이크로초를 사용하기 위해선 가장 높은 정밀도(6)을 사용해야한다

```
ex> 
CREATE TABLE `test` (
	`idx` INT(11) NOT NULL AUTO_INCREMENT,
	`dt` DATETIME(6) NULL DEFAULT NULL,
	PRIMARY KEY (`idx`)
)
ENGINE=InnoDB;

INSERT INTO test_tb(dt) VALUES (NOW()) , (NOW(6))
```

- CURRENT_TIMESTAMP() 함수가 NOW() 함수의 동의어