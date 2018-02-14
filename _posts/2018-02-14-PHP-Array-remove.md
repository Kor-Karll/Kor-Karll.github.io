---
layout: post
title: "[PHP] 배열 내 요소 제거하기"
category: PHP
tags:
- PHP
- Array
- 배열
- 배열조작
lastmod : 2018-02-14 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***



PHP 에는 요소를 제거하는 방법에는 두가지가 있는데

* array_slice() 함수

  이 함수는 특정요소에 특정값을 세팅할수도 있는 장점이 있다.
  특징은 현재 배열이 자동으로 재정렬된다.
  그래서 for문을 돌리며 요소를 제거하거나 조작할때 유의하여야한다.

* unset() 함수

  이 함수는 배열을 재정렬하지 않는다.
<!--미리보기-->

예:
```
 $temp = Array('a','b','c','d');

unset($temp[1]);

echo $temp;

$temp = [0] => 'a'
                [2] => 'c'
                [3] => 'd'
```
정렬을 원하면 array_values() 함수를 사용하면 정렬이 가능하다.
