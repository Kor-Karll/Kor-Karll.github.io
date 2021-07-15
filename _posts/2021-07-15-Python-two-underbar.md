---
layout: post
title: "[Python] 파이썬에서의 밑줄"
category: Python
tags:
- Python
- underbar
- private
lastmod : 2021-07-15 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

파이썬에서 객체의 모든 속성은 public 이다.

<!--미리보기-->

하나 _ 다른 언어의 private 개념 (하지만 public 접근 가능)

둘 __ 하나와 비슷한 개념이지만 두개를 사용하면 이름 맹글링을 거친다.

- 이름 맹글링(name mangling)
  
  _<class-name>__<attribute-name> 과 같은 이름의 속성으로 변경

ex>

``` python
class Connector:
  def __init__(self, source):
    self.source = source
    self._timeout = 60
    self.__timeout2 = 120

conn = Connector("postgresql://localhost")
conn.source
-> 'postgresql://localhost'

conn._timeout
-> 60

conn._Connector__timeout2
-> 120
```

위와 같이 이름만 변경될뿐 접근 가능하다..

참고: (책) 파이썬 클린코드
