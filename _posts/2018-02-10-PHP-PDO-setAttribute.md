---
layout: post
title: "[PHP] PDO::setAttribute 정리"
category: PHP
tags:
- PDO
- 속성
- DB
- PHP
lastmod : 2018-02-10 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

※ 영어도 더럽게 못하고 개념도 없기때문에 틀렸을 수 있습니다.

> 원문  :

```
PDO::ATTR_CASE: Force column names to a specific case.

PDO::CASE_LOWER: Force column names to lower case.

PDO::CASE_NATURAL: Leave column names as returned by the database driver.

PDO::CASE_UPPER: Force column names to upper case.
```

- PDO::ATTR_CASE 특별히 컬럼 이름을 바꾸고 싶을때 사용
- PDO::CASE_LOWER 컬럼이름을 소문자로 세팅
- PDO::CASE_NATURAL 컬럼이름을 데이터베이스에서 지정한 이름으로 세팅
- PDO::CASE_UPPER 컬럼이름을 대문자로 세팅

<!--미리보기-->

> 원문  :

```
PDO::ATTR_ERRMODE: Error reporting.

PDO::ERRMODE_SILENT: Just set error codes.

PDO::ERRMODE_WARNING: Raise E_WARNING.

PDO::ERRMODE_EXCEPTION: Throw exceptions.

PDO::ATTR_ERRMODE 에러를 보고한다.
```

 - PDO::ERRMODE_SILENT 그냥 둔다
 - PDO::ERRMODE_WARNING 로그에 워닝을 찍는다
 - PDO::ERRMODE_EXCEPTION 예외처리로 던진다

> 원문  :

```
PDO::ATTR_ORACLE_NULLS (available with all drivers, not just Oracle): Conversion of NULL and empty strings.

PDO::NULL_NATURAL: No conversion.

PDO::NULL_EMPTY_STRING: Empty string is converted to NULL.

PDO::NULL_TO_STRING: NULL is converted to an empty string.
```

- PDO::ATTR_ORACLE_NULLS 'null' 값 처리 방식
- PDO::NULL_NATURAL 변환하지 않는다.
-  PDO::NULL_EMPTY_STRING 빈문자열을 'null' 로 변환
-  PDO::NULL_TO_STRING 'null' 값을 빈문자열로 변환

> 원문  :

```
PDO::ATTR_STRINGIFY_FETCHES: Convert numeric values to strings when fetching. Requires bool.
```

- POD::ATTR_STRINGIFY_FETCHES 숫자 값을 가져올때 STRING 형태로 변환 / 옵션으로 TRUE FALSE 를 줘야함

> 원문  :

```
PDO::ATTR_STATEMENT_CLASS: Set user-supplied statement class derived from PDOStatement. Cannot be used with persistent PDO instances. Requires array(string classname, array(mixed constructor_args)).
```

- PDO::ATTR_STATEMENT_CLASS 해석안됨, 이해안됨 

구글 번역기 -> PDOStatement에서 파생 된 설정 사용자가 제공 한 문 클래스입니다. 지속적인 PDO 인스턴스와 함께 사용할 수 없습니다. 배열 (문자열 클래스 이름, 배열 (혼합 생성자 인수를))이 필요합니다.

> 원문  :

```
PDO::ATTR_TIMEOUT: Specifies the timeout duration in seconds. Not all drivers support this option, and its meaning may differ from driver to driver. For example, sqlite will wait for up to this time value before giving up on obtaining an writable lock, but other drivers may interpret this as a connect or a read timeout interval. Requires int.
```

- PDO::ATTR_TIMEOUT 제한 시간을 준다. INT 값이 필요하다 (INT 값은 초단위)


> 원문  :

```
PDO::ATTR_AUTOCOMMIT (available in OCI, Firebird and MySQL): Whether to autocommit every single statement.
```

- PDO:ATTR_AUTOCOMMIT 싱글 statement 에 대해서 매번 자동 commit 을 세팅 (OCI,Firebird,MySQL 에서 사용가능)

> 원문  :

```
PDO::ATTR_EMULATE_PREPARES Enables or disables emulation of prepared statements. Some drivers do not support native prepared statements or have limited support for them. Use this setting to force PDO to either always emulate prepared statements (if TRUE), or to try to use native prepared statements (if FALSE). It will always fall back to emulating the prepared statement if the driver cannot successfully prepare the current query. Requires bool.
```

- PDO::ATTR_EMULATE_PREPARES 준비된 statement 에뮬레이션을 사용할지 말지 결정 TRUE OR FALSE 값 필요

> 원문  :

```
PDO::MYSQL_ATTR_USE_BUFFERED_QUERY (available in MySQL): Use buffered queries.
```

- PDO::MYSQL_ATTR_USE_BUFFERED_QUEY 속성을 TRUE 로 설정하면 MySQL 드라이버는 버퍼 버전의 MySQL API를 사용한다.

> 원문  :

```
PDO::ATTR_DEFAULT_FETCH_MODE: Set default fetch mode. Description of modes is available in PDOStatement::fetch() documentation.
```

- PDO::ATTR_DEFAULT_FETCH_MODE 가져올 값에 대한 설정을 디폴트로 설정을 한다.



