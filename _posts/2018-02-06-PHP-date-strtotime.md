---
layout: post
title: "PHP date 와 strtotime 사용기"
`: PHP
tags:
- PHP
- date
- strtotime
- 시간
lastmod : 2018-02-06 14:01:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

현재 시간을 불러와 일정 조건에 의해 시간을 가공해야 하는 상황이 생겼다.

현재시간은 

```php
$today = date("Ymd His",time());
```

<!--미리보기-->

으로 생성했고

```php
if("조건"){
  $today = strtotime($today."-1 hours");
}

echo $today;
```

하였더니 계속 19700101 090000 이 찍혔다. 

```php
// 이유는 바로 이곳
$today = strtotime($today."-1 hours");
```


```php
$today = strtotime($today." -1 hours");
//이렇게 공백을 주니 제대로 출력이 되었다.
```

strtotime 이라는 함수 이름처럼 string 형태를 시간형태로 분석하여 바꿔주는것인데 시간형태에 2016-09-09 와 같이 "-" 가 들어있으면 시간형태로 인식하는것 같다.

그리고 다른 문제 하나가 더 발생하였는데

사실 위 코드처럼 전체 시간을 찍지않고 Hours 만 필요하였기에

```php
$today = date("Ymd H",time());
//위와 같이 생성하여
$today = strtotime($today."-1 hours");
//이렇게 가공하려 했다.
```

이것도 마찬가지로 19700101 090000 이 찍혔다.strtotime이 제대로 작동하지 않았다는 뜻인데,strtotime 을 이용하여 시간을 연산하려면 최소 분까지는 변수로 들어가야하는것같다.

참고 : [타임스탬프 개념](http://allenjeon.tistory.com/235)