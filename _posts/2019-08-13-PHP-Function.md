---
layout: post
title: PHP 유용한 함수들
category: PHP
tags:
- PHP
- 함수
- Function

lastmod : 2019-08-13 15:00:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->
### call_user_func(callable $callback [, mixed $... ] ) : mixed
- 사용자가 지정한 함수 적용 (php 기본 함수도 호출 가능)

``` php
function barber($type)
{
    echo "You wanted a $type haircut, no problem\n";
}
call_user_func('barber', "mushroom");
call_user_func('barber', "shave");
```

- 결과
```
You wanted a mushroom haircut, no problem
You wanted a shave haircut, no problem
```

### addslashes(string $str ) : string
- ' 같은 문자열이 있을경우 \' 형식으로 바꿔줌

```php
$str = "Is your name O'Reilly?";

// Outputs: Is your name O\'Reilly?
echo addslashes($str);
```

### extract(array &$array [, int $flags = EXTR_OVERWRITE [, string $prefix = NULL ]] ) : int)
- 배열의 key 가 변수명이 되고 value 가 변수에 값으로 할당된다
- Warning Do not use extract() on untrusted data, like user input (e.g. $_GET, $_FILES).
- 사용자 입력과 같은 신뢰할 수없는 데이터에는 extract ()를 사용하지 마십시오 라고 경고 하고 있다.

```php
$size = "large";
$var_array = array("color" => "blue",
                   "size"  => "medium",
                   "shape" => "sphere");
extract($var_array, EXTR_PREFIX_SAME, "wddx");

echo "$color, $size, $shape, $wddx_size\n";
```

결과
```
blue, large, sphere, medium
```

### function_exists(string $function_name ) : bool)
- 함수 존재유무 판단 함수

```php
if (function_exists('imap_open')) {
    echo "IMAP functions are available.<br />\n";
} else {
    echo "IMAP functions are not available.<br />\n";
}
```

### ini_get(string $varname ) : string
- PHP 구성 옵션의 값을 가져옴

```php
$max_input_vars = ini_get('max_input_vars');

    if($max_input_vars) {
        $post_vars = count($_POST, COUNT_RECURSIVE);
        $get_vars = count($_GET, COUNT_RECURSIVE);
        $cookie_vars = count($_COOKIE, COUNT_RECURSIVE);

        $input_vars = $post_vars + $get_vars + $cookie_vars;

        if($input_vars > $max_input_vars) {
            alert('폼에서 전송된 변수의 개수가 max_input_vars 값보다 큽니다.\\n전송된 값중 일부는 유실되어 DB에 기록될 수 있습니다.\\n\\n문제를 해결하기 위해서는 서버 php.ini의 max_input_vars 값을 변경하십시오.');
        }
    }
```

### strtr(string $str , array $replace_pairs ) : string
- 문자,문자열 바꾸기

```php
$trans = array("h" => "-", "hello" => "hi", "hi" => "hello");
echo strtr("hi all, I said hello", $trans);
```
결과
```
hello all, I said hi
```

