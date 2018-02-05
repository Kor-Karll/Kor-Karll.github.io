---
layout: post
title: Django Ajax 통신하기
category: Django
tags:
- Django
- Ajax
- CSRF보안
- JSON
lastmod : 2018-02-05 12:12:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

# 조건

* 넘길 값을 json 형태로 보낸다
* csrftoken 기능도 사용한다
* return 형태는 json 형태로 리턴한다

<!--미리보기-->

> ajaxtest.html

```javascript{% raw %}
// Ajax를 쓰기 위해 html 에서 jquery를 로드한다
<script src="js/jquery-2.2.3.min.js"></script>

// 보낼 데이터
jsonObj = {}
jsonObj['Key1'] = $('#Key1').val();
jsonObj['Key2'] = $('#Key2').val();

// ajax 부분
$.ajax({
  method: "POST",
  dataType : "json",
  url: "{% url 'ajaxtest:ajaxtest_def' %}",
  data:  { "jsonData" : JSON.stringify(jsonObj), "csrfmiddlewaretoken" : "{{ csrf_token }}" },
  // csrf token 을 함께 보낸다
}).done(function( msg ) {
  // 결과값 콘솔에 표시
  console.log(msg);  
});

```{% endraw %}



> ajaxtest\urls.py

``` python
urlpatterns = [
    path('ajaxtest', ajaxtest_def , name = 'ajaxtest')
]
```

> ajaxtest\views.py

``` python
from django.views.decorators.http import require_POST
from django.http import JsonResponse
import json

# 포스트 형태만 받는다
@require_POST
def ajaxtest_def(request):
    json_data = json.loads(request.POST['jsonData'])

    ###
    # 처리할 로직 부분
    ###

    return_data = {'result': 'success'}

    return JsonResponse(return_data)
```