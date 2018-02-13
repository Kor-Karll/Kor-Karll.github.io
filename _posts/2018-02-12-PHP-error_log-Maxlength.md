---
layout: post
title: "[PHP] error_log 최대길이에 대하여.. "
category: PHP
tags:
- PHP
- error_log
lastmod : 2018-02-12 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

```php
//php 로 개발하면서 가장 많이 아래와 같이 사용한다
error_log(print_r($test_value,true));

// 혹은 에러 발생시 로그파일로 남기기위해 아래와 같이 사용하기도 한다
error_log($error_code , 3 , $file);
```
<!--미리보기-->

이번에 겪은 문제는 어떤 조건에 의해 쿼리에 값을 넣어 쿼리를 만들고 그 해당 쿼리로 데이터를 조회해야하는 상황이었는데

> ※그래서 쿼리가 굉장히 길다..ㅡㅡ;

DB 문법오류가 계속 발생했다

에러로그파일로 오류가 발생했을시 해당 쿼리를 기록하게 되어있는데

쿼리 중 소실된 문자들이 보였다

문제 요소는 2가지라고 생각했는데

* PHP String 자체의 최대길이 제한
* PHP PDO 에서 쿼리 최대길이 제한

이라고 생각 했다

두 부분 모두 테스트 해봤지만 둘 다 해당이 아니였고,

알고 보니 쿼리 자체를 잘못 조합한거였다.

게다가 error_log 로 파일로 만들때 쿼리문자열 중 일부가 소실되는거였다.

찾아보니 error_log로 남길수있는 최대 길이가 있었다.

```
Set the maximum length of log_errors in bytes. In error_log information about the source is added. The default is 1024 and 0 allows to not apply any maximum length at all. This length is applied to logged errors, displayed errors and also to $php_errormsg.

When an integer is used, the value is measured in bytes. Shorthand notation, as described in this FAQ, may also be used.
```

아래와 같이 세팅하면 무제한이다!

```
ini_set('log_errors_max_len', 0);
```

참고 : [http://php.net/manual/en/errorfunc.configuration.php#ini.log-errors-max-len](http://php.net/manual/en/errorfunc.configuration.php#ini.log-errors-max-len)