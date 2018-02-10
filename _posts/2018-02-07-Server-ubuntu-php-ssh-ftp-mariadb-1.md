---
layout: post
title: 서버구축 1번째 NUC[DN2820FYKH](ubuntu 14.04/php/ssh/ftp/mariadb)
category: Server
tags:
- ubuntu
- setting
- 서버 구축
lastmod : 2018-02-07 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

우분투 14.04 OS설치 후

```
$sudo apt-get update

$sudo apt-get upgrade #실행해 최신버전 업데이트
```

<!--미리보기-->

* FTP 서버 설치

```
$sudo apt-get install vsftpd (설치)
```

```
$sudo vi /etc/vsftpd.conf (설정)

-> anonymouse_enable=NO : 임의사용자,로컬사용자 둘다 접속 불가능

    local_enable=YES : 계정에 원격접속 가능함

    write_enable=YES

    local_umask=022

$ifconfig 로 주소확인 후  putty로 접속
```


* WebServer 설치

1. Apache 설치

```
$sudo apt-get install apache2
```

2. 설치 확인방법

```
$ifconfig
```

- p2p1의 inet addr 확인(브라우저로 접속해 보면)

![브라우저 화면]({{ site.baseurl }}/images/posts/2018-02-07-Server-ubuntu-php-ssh-ftp-mariadb-1/1.PNG)

이런 화면이 뜬다



* 서버 도메인명 지정

```
$sudo vi /etc/apache2/apache2.conf



-> #fully qualified domain name,using 127.0.1.1 for ServerName

   ServerName localhost (항목추가)
```


3. 기본페이지 바꾸기

```
$sudo vi /etc/apache2/site-enabled/000-default.conf



-> DocumentRoot /var/www/html (로 되어있다.)

   => DocumentRoot /var/www/ 로 수정
```


 4. Apache  시작과 종료방법


```
$sudo /etc/init.d/apache2 stop

$sudo /etc/init.d/apache2 start

$sudo /etc/init.d/apache2 restart
```


* PHP 설치


```
$sudo apt-get install php5 (14.04버전이라 그런지 php7이 안깔린다..)
```


암호화 모듈

```
$sudo apt-get install php5-mcrypt
```


이미지처리 모듈

```
$sudo apt-get install php5-gd
```


원격지 정보 불러는 모듈 (워드프레스, 드루팔 등에서 쓰임)

```
$sudo apt-get install php5-curl
```


추가로 설치하고 싶은 모듈이 있으면

```
$sudo apt-cache search php5-
```


아파치 재시작(적용)

```
$sudo service apache2 restart
```


* MariaDB 설치


```
$sudo apt-get install mariadb-server-5.5
```

![linux 화면]({{ site.baseurl }}/images/posts/2018-02-07-Server-ubuntu-php-ssh-ftp-mariadb-1/2.PNG)

위 그림처럼 화면이 뜨면 패스워드 설정후 계속 진행

```
$sudo apt-get install mariadb-client-5.5

$sudo apt-get install php5-mysql
```


mariadb 실행

```
$sudo service mysql start

$mysql -u root -p
```

로 제대로 실행되는지 확인

```
status 로 상태확인시



mysql  Ver 15.1 Distrib 5.5.49-MariaDB, for debian-linux-gnu (x86_64) using readline 5.2

Connection id:          39

Current database:

Current user:           root@localhost

SSL:                    Not in use

Current pager:          stdout

Using outfile:          ''

Using delimiter:        ;

Server:                 MariaDB

Server version:         5.5.49-MariaDB-1ubuntu0.14.04.1 (Ubuntu)

Protocol version:       10

Connection:             Localhost via UNIX socket

Server characterset:    latin1

Db     characterset:    latin1

Client characterset:    utf8

Conn.  characterset:    utf8

UNIX socket:            /var/run/mysqld/mysqld.sock

Uptime:                 22 min 0 sec



Threads: 1  Questions: 583  Slow queries: 0  Opens: 182  Flush tables: 4  Open tables: 24  Queries per second avg: 0.441
```

위와 같이 문자셋이 전부 라틴1로 되어있다.

* Mariadb 설정 바꾸기

```
$ sudo vi /etc/mysql/my.cnf
  ->[mysqld] 항목에
     character-set-server = utf8 (추가)
     bind-address = 127.0.0.1 로 되어있다(접속가능주소) => bind-address = * 로 수정하면 외부에서도 접속가능하다.
     [mysql] 항목에
     default-character-set = utf8 (추가)
     
$sudo service mysql restart (mariadb 다시 시작)
```

다시 들어가 status 로 확인해보면 latin1->utf8로 바껴있는걸 확인할수있다.

