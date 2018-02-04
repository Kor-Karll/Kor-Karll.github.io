---
layout: post
title: [Python] 문법 %?
category: Python
tags:
- Python
- 문법
- Fommating String
lastmod : 2018-02-03 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

책을 보던중

```python
schWord = '%s' % self.request.POST['search_word']
```

<!--미리보기-->

위와 같이 %가 있는 코드를 보았다. ''안에 있는 문구는 정규식인거 같은데 뒤에 %는 무슨내용인지 알수가 없었다.

그래서 찾아보았더니!

It is a string formatting syntax (which it borrows from C).

Please see "Formatting Strings":

Python supports formatting values into strings. Although this can include very complicated expressions, the most basic usage is to insert values into a string with the %s placeholder.

Edit: Here is a really simple example:

``` python
name = raw_input("who are you?")
print "hello %s" % (name,)
```

출처 : 
<a href="https://stackoverflow.com/questions/997797/what-does-s-mean-in-python">
https://stackoverflow.com/questions/997797/what-does-s-mean-in-python
</a>

Fomatting Strings 란다.

쿼리문에 파라미터 바인딩 시키듯이 사용하는것 같다.