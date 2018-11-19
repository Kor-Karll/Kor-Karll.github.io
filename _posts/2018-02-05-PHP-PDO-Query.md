---
layout: post
title: PDO 멀티 쿼리 날리기
category: PHP
tags:
- PHP
- PDO
- 쿼리
lastmod : 2018-02-05 15:51:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

```php
$conn = new \PDO("설정값"); // 커넥션 맺기

$conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

$conn->setAttribute(PDO::MYSQL_ATTR_INIT_COMMAND,'SET NAMES utf8');
```

<!--미리보기-->

멀티 쿼리가 가능하게 하는부분 true면 prepare statement 를 사용한것과 같이 query를 사용

```php
$conn->setAttribute(PDO::ATTR_EMULATE_PREPARES, true);

for("조건"){

  $query = "SELECT1 ;   SELECT2 ; SELECT3 ;  ";

}

$stmt = $conn->query($query);
```

컬럼을 카운트하여 rowset에 데이터가 있는지 판단

```php
while($stmt->columnCount){

  $result = $stmt->fetchAll(\PDO::FETCH_ASSOC);

  if (count($result) > 0) {

  break;

  }

  else $stmt->nextRowSet();

}
```

참고 : [PHP:PDO::setAttribute - Manual](http://php.net/manual/kr/pdo.setattribute.php)


