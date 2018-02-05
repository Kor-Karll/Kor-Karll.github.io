---
layout: post
title: PHP 위험제거,유효성 검사,예외 처리
category: PHP
tags:
- PHP
- 유효성 검사
- 예외처리
lastmod : 2018-02-05 15:16:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

# 위험값 제거 

  - 입력데이터가 애플리케이션 저장소 계층에 도달하기 전에 위험을 제거

ex)
```
<script>태그 댓글 허용 금지
```

<!--미리보기-->


# HTML

- HTML 특수문자 (예:&,>,;>는 htmlentitie() 함수를 이용해서 각각에 해당하는 HTML 엔티티로 교체



# SQL 쿼리

- 대부분의 SQL데이터베이스가 --를 주석 시작으로 간주

  악의적으로 --가 포함된 스크립트를 보내면 문제발생

  입력데이터를 SQL쿼리에 합쳐야한다면 준비된 PDO문을 사용

# 사용자 정보

- 사용자 계정의 이메일,전화번호,우편번호등의 신상정보는 filter_var()와 filter_input() 함수를 사용

* 자세한내용은 [http://php.net/manual/function.filter-var.php](http://php.net/manual/function.filter-var.php) 참고



# 유효성 검사

- 입력데이터가 안전하며 기대했던 데이터가 맞는지 확인하려면 입력 데이터의 유효성을 검사하고 위험을 제거해야 한다.

  PHP 기본 함수 filter_var()와 다음 유효성 검사도구들 추천

* [aura/filter](http://packagist.org/packages/aura/filter) 

* [respect/validation](http://packagist.org/packages/respect/validation) 

* [symfony/validator](http://packagist.org/packages/symfony/validator)



# 출력 예외 처리

- htmlentities() 함수를 이용하여 출력 예외처리 또는 PHP 템플릿으로 자동 출력예외처리.

* 자동 출력예외처리 PHP템플릿 

 - [twig/twig](http://packagist.org/packages/twig/twig)  특별히 지정하지 않는 한 기본적으로 모든 출력 예외처리

 - [smarty/smarty](http://packagist.org/packages/smarty/smarty)

