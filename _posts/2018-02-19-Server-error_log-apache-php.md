---
layout: post
title: "[Server] error_log (apache) 에서 array 값 찍기"
category: Server
tags:
- Server
- PHP
- error_log
- apache
lastmod : 2018-02-19 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

서버 프로그램으로 apache를 사용중인데 error_log 로 array를 찍을때 print_r을 이용해 찍었더니

<!--미리보기-->

```
[Thu Sep 29 21:39:11.299654 2016] [:error] [pid 15942] [client 111.111.0.1111:111111] Array\n(\n    [0] => Array\n        (\n            [0] => \xeb\xa9\x94\xeb\xb0\x80\n        )\n\n    [1] => Array\n        (\n            [0] => \xeb\x95\x85\xec\xbd\xa9\n        )\n\n    [2] => Array\n        (\n            [0] => \xeb\x8c\x80\xeb\x91\x90\n        )\n\n)\n
```

이런식으로 알아보기 힘들게 나왔다.

nginx 는 

```
[Thu Sep 29 21:39:11.299654 2016] [:error] [pid 15942] [client 192.168.0.1:57687] Array

(
    [0] => Array

        (
            [0] => \xeb\xa9\x94\xeb\xb0\x80
        )

    [1] => Array

        (
            [0] => \xeb\x95\x85\xec\xbd\xa9
        )

    [2] => Array

        (
            [0] => \xeb\x8c\x80\xeb\x91\x90
        )
)
```

이런식으로 잘 나왔는데 apache 는 저런 형식으로 출력이 안돼는것 같다.

그래서 error_log 에서 array 를 찍을때 포멧을 변경할수있는지 검색해 봤는데 내가 못찾는건지 찾기가 힘들었다.

결국 찾아낸 방법은 tail 문에서 해결하는거..

```
tail -f /var/log/apache2/error.log | sed -e 's/\\n/\n/g'
```

위와 같이 쓰면 nginx 처럼 알아보기 편하게 출력이 가능하다.
