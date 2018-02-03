---
layout: post
title: "[Python] *args and **kwargs?"
category: Python
tags:
- Python
- args
- kwargs
- 임의인자
lastmod : 2018-02-03 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

*args = list

**kwargs = dictionary

두개 다 임의의 인자(몇개가 들어올지 모르는 인자)를 사용해야할 때 사용한다
<!--미리보기-->
ex> *args
``` python
def print_everything(*args):
  for count, thing in enumerate(args):
  ... print( '{0}. {1}'.format(count, thing))
  ... 
print_everything('apple', 'banana', 'cabbage')
```
result :
```
0. apple
1. banana
2. cabbage
```
ex> **kwargs
``` python
def table_things(**kwargs):
  for name, value in kwargs.items():
    print( '{0} = {1}'.format(name, value))

table_things(apple = 'fruit', cabbage = 'vegetable')
```
result :
```
cabbage = vegetable
apple = fruit
```
참고:<a href="https://stackoverflow.com/questions/3394835/args-and-kwargs">Link</a>
