---
layout: post
title: PHP 날짜,시간,시간대
`: PHP
tags:
- PHP
- Timezone
lastmod : 2018-02-05 15:23:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

PHP 5.2.0 에 도입된 DateTime,DateInterval,DateTimeZone 클래스 사용

이 함수들을 사용하려면 기본시간지정해야함.

<!--미리보기-->

ex> date.timezone = 'Asia/Seoul';

date_defaul_timezone_set() 함수를 이용하면 런타임 시에 기본 시간대 설정 가능

시간대식별자는 [http://php.net/manual/timezones.php](http://php.net/manual/timezones.php) 에서 전체목록 확인가능

- DateTime 클래스

```php
 $datetime = new DateTime();
```

위와 같이 인자를 주지않으면 현재시간으로 생성.

사용자 정의형식으로 포멧설정가능

```php
$datetime = DateTime::createrFromFormat('M j,Y H:i:s', 'Jan 5, 2016 20:08:54');
```

- DateInterval 클래스

DateTime 인스턴스를 조작하는데 사용
```php
$datetime = new DateTime('2016-02-02 16:00:00'); < DateTime인스턴스 생성 >
     $interval = new DateInterval('P2W'); < 두 주 간격 생성 >
     $datetime->add($interval); < DateTime 인스턴스 수정 >
     echo $datetime->format('Y-m-d H:i:s');
```

- DateTimeZone 클래스

시간대를 나타낸다. 생성자에 유효한 식별자 전달하면 된다.

```php
$timezone = new DateTimezone('Asia/Seoul');
     $datetime = new DateTime('2016-08-08' , $timezone);
```

- DatePeriod 클래스

반복 일정에 사용하면 좋음, 세가지 필수 인수

 + 반복이 시작되는 일시를 나타내는 DateTime 인스턴스
 + 반복되는 일시 사이의 시간 간격을 나타내는 DateInterval 인스턴스
 + 반복될 횟수를 나타내는 정수