---
layout: post
title: "[Web] jQuery 셀렉터"
category: Web
tags:
- Web
- jQuery
- Selector
lastmod : 2019-07-29 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->

<pre>
#jquery         // id 선택자 <br>
.tutorial       // class 선택자 <br>
li              // 엘리먼트 선택자 <br>
#jquery, #MYSQL // 다중 선택자 <br>
</pre>

<hr>

```HTML
<ul id='list'>
    <li> HTML </li>
    <li> CSS </li>
    <li> javascript </li>
    <li> PHP </li>
    <li> MYSQL </li>
</ul>
```
<pre>
#list li:eq(2)  // 인자와 인덱스가 동일한 엘리먼트를 찾아내는 선택자    -> javascript
#list li:gt(1)  // 인자보다 인덱스가 큰 엘리먼트를 찾아내는 선택자      -> javascript.PHP,MYSQL  
#list li:lt(2)  // 인자보다 인덱스가 작은 엘리먼트를 찾아내는 선택자    -> HTML,CSS
#list li:even   // 홀수의 인덱스 값을 가진 엘리먼트에 대한 선택자       -> HTML,javascript,MYSQL
#list li:odd    // 짝수의 인덱스 값을 가진 엘리먼트에 대한 선택자       -> CSS,PHP
#list li:first  // 첫번째 인덱스 엘리먼트에 대한 선택자                 -> HTML
#list li:last   // 마지막 인덱스 엘리먼트에 대한 선택자                 -> MYSQL
</pre>

<hr>

```HTML
<ul id='attribute'>
    <li target='ABCD'>ABCD</li>
    <li target='BCDE'>BCDE</li>
    <li target='CDEF'>CDEF</li>
    <li target='DEFG'>DEFG</li>
    <li target='EFGH'>EFGH</li>
    <li id='FGHI' target='FGHI'>FGHI</li>
</ul>
```
<pre>
[target*='BC']      // 속성의 값에 주어진 문자열이 포함되는 엘리먼트를 찾아내는 선택자                 -> ABCD,BCDE
[target='DEFG']     // 속성의 값과 주어진 문자열이 일치하는 엘리먼트를 찾아내는 선택자                 -> DEFG
[target!='DEFG']    // 속성의 값과 주어진 문자열이 일치하지 않는 엘리먼트를 찾아내는 선택자            -> ABCD,BCDE,CDEF,EFGH,FGHI
[target^='B']       // 속성의 값으로 주어진 문자열이 처음 등장하는 엘리먼트를 찾아내는 선택자          -> BCDE
[target$='H']       // 속성의 값으로 주어진 문자열이 마지막으로 등장하는 엘리먼트를 찾아내는 선택자    -> EFGH
[target]            // 속성이 존재하는 엘리먼트를 찾아내는 선택자                                   -> ABCD,BCDE,CDEF,DEFG,EFGH,FGHI
[target][id]        // 속성들이 존재하는 엘리먼트를 찾아내는 선택자                                 -> FGHI
</pre>

<hr>

```HTML
<div>
    <input type='text' disabled='disabled' value='disabled'>
    <input type='text' value='enabled'>
</div>
<div><input type='checkbox' checked='checked'/></div>
<div><input type='checkbox'/></div>
```
<pre>
[type='text']               // 폼 엘리먼트를 선택할때는 속성 셀렉터를 사용한다
[type='text']:disabled      // disabled 속성 값이 disabled인 엘리먼트를 찾아내는 선택자
[type='text']:enabled       // disabled 속성 값이 enabled인 엘리먼트를 찾아내는 선택자
input:checked               // 체크박스 중 체크가 된 엘리먼트를 찾아내는 선택자
</pre>