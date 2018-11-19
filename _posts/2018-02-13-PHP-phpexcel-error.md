---
layout: post
title: "[PHP] phpexcel 'simplexml_load_string' 에러 "
`: PHP
tags:
- phpexcel
- PHP
- error
lastmod : 2018-02-13 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->

```
[Wed Oct 12 12:52:16.743703 2016] [:error] [pid 7548] [client 192.168.0.1:49828] PHP Fatal error:  Uncaught Error: Call to undefined function simplexml_load_string() in /경로/PHPExcel_1.8.0_doc/Classes/PHPExcel/Reader/Excel2007.php:97

Stack trace:

#0 /경로/PHPExcel_1.8.0_doc/Classes/PHPExcel/IOFactory.php(268): PHPExcel_Reader_Excel2007->canRead('./download/exce...')

#1 /경로/PHPExcel_1.8.0_doc/Classes/PHPExcel/IOFactory.php(205): PHPExcel_IOFactory::createReaderForFile('./download/exce...')

#2 /경로/phpexceltest.php(62): PHPExcel_IOFactory::identify('./download/exce...')

#3 {main}

  thrown in /경로/PHPExcel_1.8.0_doc/Classes/PHPExcel/Reader/Excel2007.php on line 97, referer: http://주소/phpexcelview.php
```

뷰부분 파일 phpexcelview.php

로직부분 파일 phpexceltest.php

Excel2007 버전 이하 엑셀파일은 다 잘 읽어오는데 그 이상버전 엑셀파일을 업로드 후에 읽을때 계속 위와 같은 에러가 발생하였다.

Google 신께 여쭤봤지만 나같은 증상을 겪는 사람이 없는건지 영어가 딸려서 못찾는건지 못찾던중

simplexml_load_string 을 검색하면 하나같이 phpexcel 과는 전혀 다른 내용만 검색되는걸 확인하였다..

phpexcel 문제가 아닌 php 문제였던것이다..;

php 의 필요한 기능만 설치하였는데 그중 php-xml 이 설치가 안돼서 저 오류가 발생했던거다.

php-xml 을 설치하니 문제가 해결되었다.

삽질시간 : 5시간..


