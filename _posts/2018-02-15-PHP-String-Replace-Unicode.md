---
layout: post
title: "[PHP] 문자치환 / 유니코드 / 정규식"
category: PHP
tags:
- PHP
- 문자열조작
- 유니코드
- 정규식
lastmod : 2018-02-15 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***



웹에서 글을 입력받아 DB에 저장한후 웹과 앱에서 호출하여 보여주는 서비스가 필요했다.

또, 글을 '다.' 와 개행 등의 조건으로 문장으로 쪼개어 해당 길이 및 시작점과 끝점을 같이 저장하여 앱에서 각 문장을 선택이나 해제할수 있게 해야했다.

안드로이드 TextView에서는 자동으로 개행을 하는데 공백이 있거나 한자가 있으면 이상하게 개행을 자동으로 했다.

<!--미리보기-->

그래서 공백과 각문자별로 문자치환,문자삽입(유니코드)를 해야했는데

```php
<?php
// 공백치환
$content = preg_replace('/ /','\\u00a0',$content);
?>
```

위 함수를 사용하여 치환하면 '\\u00a0' 이 유니코드가 아닌 문자열 그대로 치환이 되었다.
(어찌보면 당연한거였다..)

함수의 문제라 생각하여 str_replace,preg_replace,mb_ereg_replace 모두 사용해보았지만 문자열 그대로 치환이 되었다.

```javascript
<script>
var content = $('#content').val().replace(/ /g, '\u00a0');
</script>
```

위와 같이 자바스크립트에서는 그냥 문자에 유니코드로 치환하는게 되어서 php도 될거라고 생각한게 잘못이었다.

```php
<?php
$content_json = json_encode($content);

$content = preg_replace('/ /','\\u00a0',$content_json); // 공백치환
$content = preg_replace('/\\\u..../','\\0\u200b',$content); // 각문자별 치환
$content = preg_replace('/\\\ub2e4\\\u200b\\./','\\ub2e4.',$content); // 다. 치환
$content = json_decode($content);
?>
```

위와 같이 유니코드로 변환후 문자치환을 하고 다시 변환하는 방식으로 해결하였다.

※ 정규식은 각문자가 유니코드로 변환했을때 '\uXXXX' 와 같은 형식을 선택해야했는데 preg_replace 함수에서 \\를 써야 뒤에 오는것을 문자로 인식한다 해서 \\\u.... 으로 선택하면된다.