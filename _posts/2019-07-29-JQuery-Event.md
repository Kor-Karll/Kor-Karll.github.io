---
layout: post
title: "[Web] jQuery 이벤트"
category: Web
tags:
- Web
- jQuery
- Selector
lastmod : 2019-07-29 16:20:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->

## jQuery 의 이벤트
- 크로스브라우징의 문제를 해결
- bind 로 이벤트 핸들러를 설치하고, unbind로 제거 (예제1)
- trigger 로 이벤트 핸들러를 강제로 실행 (예제2)
- click, ready 와 같이 다양한 이벤트 헬퍼를 제공
- live 를 이용하면 현재 존재 하지 않는 엘리먼트에 이벤트 핸들러를 설치할 수 있음

<hr>
* 예제1 bind, unbind, trigger 를 이용한 이벤트의 설치, 제거, 호출

<html>
  <head>
    <script type='text/javascript' src='https://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.min.js'></script>
    <script type='text/javascript'>
      function clickHandler(e){
        alert('thank you')
      }
      $(document).bind('ready',function(){
        $('#click_me1').bind('click', clickHandler);
        $('#remove_event1').bind('',function(e){
          $('#click_me1').unbind('click', clickHandler);
        });
        $('#trigger_event1').bind('click',function(e){
          $('#click_me1').trigger('click');
        });

        $('#click_me2').bind('click', clickHandler);
        $('#remove_event2').bind('',function(e){
          $('#click_me2').unbind('click', clickHandler);
        });
        $('#trigger_event2').bind('click',function(e){
          $('#click_me2').trigger('click');
        });

        $('#click_me3').live('click', clickHandler);
        $('#remove_event3').live('',function(e){
          $('#click_me3').die('click', clickHandler);
        });
        $('#trigger_event3').live('click',function(e){
          $('#click_me3').trigger('click');
        });
      });
    </script>
  </head>
  <body>
    <input id='click_me1' type='button' value='click_me' />
    <input id='remove_event1' type='button' value='unbind' />
    <input id='trigger_event1' type='button' value='trigger' />
  </body>
</html>

```javascript
<html>
  <head>
    <script type='text/javascript' src='https://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.min.js'></script>
    <script type='text/javascript'>
      function clickHandler(e){
        alert('thank you')
      }
      $(document).bind('ready',function(){
        $('#click_me').bind('click', clickHandler);
        $('#remove_event').bind('',function(e){
          $('#click_me').unbind('click', clickHandler);
        });
        $('#trigger_event').bind('click',function(e){
          $('#click_me').trigger('click');
        });
      });
    </script>
  </head>
  <body>
    <input id='click_me' type='button' value='click_me' />
    <input id='remove_event' type='button' value='unbind' />
    <input id='trigger_event' type='button' value='trigger' />
  </body>
</html>
```

<hr>
* 예제2 이벤트 헬퍼

<html>
  <body>
    <input id='click_me2' type='button' value='click_me' />
    <input id='remove_event2' type='button' value='unbind' />
    <input id='trigger_event2' type='button' value='trigger' />
  </body>
</html>

```javascript
<html>
  <head>
    <script type='text/javascript' src='https://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.min.js'></script>
    <script type='text/javascript'>
      function clickHandler(e){
        alert('thank you')
      }
      $(document).ready(function(){
        $('#click_me').bind('click', clickHandler);
        $('#remove_event').bind('',function(e){
          $('#click_me').unbind('click', clickHandler);
        });
        $('#trigger_event').bind('click',function(e){
          $('#click_me').trigger('click');
        });
      });
    </script>
  </head>
  <body>
    <input id='click_me' type='button' value='click_me' />
    <input id='remove_event' type='button' value='unbind' />
    <input id='trigger_event' type='button' value='trigger' />
  </body>
</html>
```

<hr>
* 예제3 live 를 이용하면 존재하지 않는 엘리먼트에 대해서 이벤트를 설치할 수 있다

<html>
  <body>
    <input id='click_me3' type='button' value='click_me' />
    <input id='remove_event3' type='button' value='unbind' />
    <input id='trigger_event3' type='button' value='trigger' />
  </body>
</html>

```javascript
<html>
  <head>
    <script type='text/javascript' src='https://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.min.js'></script>
    <script type='text/javascript'>
      function clickHandler(e){
        alert('thank you')
      }
      $(document).ready(function(){
        $('#click_me').live('click', clickHandler);
        $('#remove_event').live('',function(e){
          $('#click_me').die('click', clickHandler);
        });
        $('#trigger_event').live('click',function(e){
          $('#click_me').trigger('click');
        });
      });
    </script>
  </head>
  <body>
    <input id='click_me' type='button' value='click_me' />
    <input id='remove_event' type='button' value='unbind' />
    <input id='trigger_event' type='button' value='trigger' />
  </body>
</html>
```