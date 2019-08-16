---
layout: post
title: CodeIgniter + PhpSpreadsheet 적용하기
category: PHP
tags:
- PHP
- CI
- CodeIgniter
- PhpSpreadsheet

lastmod : 2019-08-12 15:00:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->
## Step 1. CodeIgniter 설치

## Step 2. composer 로 phpoffice 설치

```
## $ composer require phpoffice/phpspreadsheet
```

CodeIgniter 설치경로 / vendor /

위 경로 아래로 설치됨

## Step 3. application/config/config.php 파일 수정

```php
$config['composer_autoload'] = 'vendor/autoload.php';
```

## Step 4. 예제 샘플 application/controller/Welcom.php

```php
defined('BASEPATH') OR exit('No direct script access allowed');
 
use PhpOffice\PhpSpreadsheet\Spreadsheet;
use PhpOffice\PhpSpreadsheet\Writer\Xlsx;
 
class Welcome extends CI_Controller {
    
    public function index()
    {       
        $spreadsheet = new Spreadsheet();
        $sheet = $spreadsheet->getActiveSheet();
        $sheet->setCellValue('A1', 'Hello World !');
        
        $writer = new Xlsx($spreadsheet);
 
        $filename = 'sample.xlsx';
 
        $writer->save($filename); 
    }
 
    public function download()
    {
        $spreadsheet = new Spreadsheet();
        $sheet = $spreadsheet->getActiveSheet();
        $sheet->setCellValue('A1', 'Hello World !');
        
        $writer = new Xlsx($spreadsheet);
 
        $filename = 'sample';
 
        header('Content-Type: application/vnd.ms-excel');
        header('Content-Disposition: attachment;filename="'. $filename .'.xlsx"'); 
        header('Cache-Control: max-age=0');
        
        $writer->save('php://output'); // download file 
 
    }
}
```

참고 : [How to generate Excel using PhpSpreadsheet in CodeIgniter](https://arjunphp.com/generate-excel-phpspreadsheet-codeigniter-php/)


