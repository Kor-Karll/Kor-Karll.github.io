---
layout: post
title: "[Web] jQuery 엘리먼트 제어"
category: Web
tags:
- Web
- jQuery
- Element
lastmod : 2019-08-01 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->

## 엘리먼트 제어
- jQuery는 엘리먼트를 제어하는 기능을 많이 제공
- http://api.jquery.com/category/manipulation/

### 자식으로 삽입(.append(), .appendTo(), .prepend(), .prependTo(), .text())

``` html
<!DOCTYPE html>
<html>
<head>
  <style>
  p{
    background:yellow;
  }
  </style>
  <script src='http://code.jquery.com/jquery-latest.js'></script>
</head>
<body>
<p>
  i would like to say:
</p>
<script>
  $('p').appned('<strong>Hello</strong>')
</script>
</body>
</html>
```

<hr>

### 형제로 삽입(.after(), .before(), .insertAfter(), .insertBefore())

``` html
<!DOCTYPE html>
<html>
<head>
  <style>
  p{
    background:yellow;
  }
  </style>
  <script src='http://code.jquery.com/jquery-latest.js'></script>
</head>
<body>
<p>
  i would like to say:
</p>
<script>
  $('p').after('<strong>Hello</strong>')
</script>
</body>
</html>
```

<hr>

### 부모로 감싸기(.unwrap(), .wrap(), .wrapAll(), .wrapInner())

``` html
<!DOCTYPE html>
<html>
<head>
  <style>
  div{
    border:2px blue solid;
    margin:2px;
    padding:2px;
  }
  p{
    background:yellow;
    margin:2px;
    padding:2px;
  }
  strong
  {
    color:red;
  }
  </style>
  <script src='http://code.jquery.com/jquery-latest.js'></script>
</head>
<body>
  <span>Span Text</span>
  <strong>What about me?</strong>
  <span>Another One</span>
<script>
  $('span').wrap('<div><div><p><em><b></b></em></p></div></div>');
</script>
</body>
</html>
```

### 삭제(.detach(), .empty(), .remove(), .unwrap())

``` html
<!DOCTYPE html>
<html>
<head>
  <style>
  div{
    border:2px blue solid;
    margin:2px;
    padding:2px;
  }
  p{
    background:yellow;
    margin:2px;
    padding:2px;
  }
  strong
  {
    color:red;
  }
  </style>
  <script src='http://code.jquery.com/jquery-latest.js'></script>
</head>
<body>
  <span>Span Text</span>
  <strong>What about me?</strong>
  <span>Another One</span>
<script>
  $('span').wrap('<div><div><p><em><b></b></em></p></div></div>');
</script>
</body>
</html>
```