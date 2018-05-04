---
layout: post
title: "[PHP] CI 세팅 관련"
category: PHP
tags:
- PHP
- CodeIgniter
lastmod : 2018-05-04 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->

1. config.php - 환경 설정

    - $config['subclass_prefix'] = 'Pre_'; // 커스텀 라이브러리 생성시 접두어 명명
    - $config['encryption_key'] = 'test1234'; // 암호화 키 설정
    - $config['sess_driver'] = 'database'; // 세션 저장 파일이 아닌 DB로 변경
    - $config['sess_cookie_name'] = 'sess_cookie'; // 세션 쿠키 이름
    - $config['sess_expiration'] = 7200; // 세션 유효시간
    - $config['sess_save_path'] = 'test_sessions'; // 세션 저장 Table 명
    - $config['sess_match_ip'] = TRUE;
    - $config['sess_time_to_update'] = 300;
    - $config['sess_regenerate_destroy'] = FALSE;
    - $config['csrf_protection'] // CSRF 설정 (모바일앱 접속시 기능 해제)
    ```
    if ( isset($_SERVER['HTTP_USER_AGENT']) && preg_match('/(iPhone|iPod|iPad|Android|BlackBerry)/',$_SERVER['HTTP_USER_AGENT']))
    {
        $config['csrf_protection'] = FALSE;
    }
    else
    {
        $config['csrf_protection'] = TRUE;
    }
    ```
    - $config['csrf_token_name'] = 'csrf_token'; // CSRF 토큰 이름
    - $config['csrf_cookie_name'] = 'csrf_cookie'; // CSRF 쿠키 이름
    - $config['csrf_expire'] = 7200; // CSRF 토큰 유효시간
    - $config['csrf_regenerate'] = FALSE; // 매 서브밋 마다 재생성 여부
    - $config['csrf_exclude_uris'] = array();

2. constants.php - 상수 설정
    - defined('SERVICE_EMAIL') OR define('SERVICE_EMAIL','noreply@test.xyz'); // 관리자 이메일 발송시 표시할 이메일주소

3. database.php - 데이터베이스 접속 설정

    ```
    $db['default'] = array(
        'dsn'	=> '',
        'hostname' => 'localhost',
        'username' => 'test',
        'password' => 'test1234',
        'database' => 'testdatabase',
        'dbdriver' => 'mysqli',
        'dbprefix' => '',
        'pconnect' => FALSE,
        'db_debug' => (ENVIRONMENT !== 'production'),
        'cache_on' => FALSE,
        'cachedir' => '',
        'char_set' => 'utf8',
        'dbcollat' => 'utf8_general_ci',
        'swap_pre' => '',
        'encrypt' => FALSE,
        'compress' => FALSE,
        'stricton' => FALSE,
        'failover' => array(),
        'save_queries' => TRUE
    );
    ```
  
4. routes.php
  - $route['default_controller'] = 'login'; // 디폴트 주소로 접속했을때 진행할 컨트롤러 지정(ex> https://test.xyz/test)