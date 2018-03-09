---
layout: post
title: MariaDB 암호화 플러그인 적용(Data at Rest Encryption)
category: DB
tags:
- MariaDB
- 암호화
- 플러그인
- DB세팅
lastmod : 2018-02-23 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

미리보기

<!--미리보기-->

- 우선 MariaDB 의 버전부터 확인한다. MariaDB 10.1.3 에서 추가되었다.

- file_key_management plugin(파일를 키로 이용하게 해주는 플러그인)

![1.jpg]({{ site.baseurl }}/images/posts/2018-02-23-DB-MariaDB-PlugIn-Encryption/1.jpg)

 * /etc/my.cnf.d/server.cnf 사용 예 :

```
[mysqld]
file_key_management_encryption_algorithm=aes_cbc
file_key_management_filename = /home/mdb/keys.enc
file_key_management_filekey = secret
```

- 키 파일 생성

 * 키 파일은 세미콜론에 의해 분리된 암호화 키 식별자(32-bit numbers) 와 hex로 인코딩된 암호화 키를 포함합니다. 128, 192 또는 256 bit 키도 지원됩니다. Comment는 hash character로 시작됩니다.

 * keys.txt 예 :

```
# this is a comment
1;770A8A65DA156D24EE2A093277530142
18;F5502320F8429037B8DAEF761B189D12F5502320F8429037B8DAEF761B189D12
```

 * 키 파일은 암호화되어질 수 있습니다. 그리고 파일을 복호화하는 키는 옵션의 file_key_management_filekey 파라미터와 함께 주어집니다.



 * 키 파일을 암호화하기 위해 OpenSSL 명령어 utility를 사용합니다. 예 :


```
openssl enc -aes-256-cbc -md sha1 -k secret -in keys.txt -out keys.enc
```

* 주의 : key 파일을 mysql 이 접근할수 있게 경로,파일 Permission 조정을 해줘야한다.

- XtraDB and InnoDB

(/etc/my.cnf.d/server.cnf/ 설정변수)

![2.jpg]({{ site.baseurl }}/images/posts/2018-02-23-DB-MariaDB-PlugIn-Encryption/2.jpg)


* XtraDB 암호화를 사용한 my.cnf 예:

```
[mysqld]
plugin-load-add=file_key_management.so
file-key-management
file-key-management-filename = /mount/usb1/keys.txt
innodb-encrypt-tables
innodb-encrypt-log
innodb-encryption-threads=4
```

- 테이블 생성시 옵션 주기

![3.jpg]({{ site.baseurl }}/images/posts/2018-02-23-DB-MariaDB-PlugIn-Encryption/3.jpg)

* 테이블 생성 예 :

```
CREATE TABLE T (id int, value varchar(255)) ENCRYPTED=YES ENCRYPTION_KEY_ID=17;
```

- table T를 key 17로 암호화하여 생성합니다.

```
ALTER TABLE T ENCRYPTED=YES ENCRYPTION_KEY_ID=18;
```

- table T를 key18로 암호화하여 변경합니다. 만약 전에 암호화가 되어있었다면 우선 복호화한 다음에 다시 암호화합니다.

```
ALTER TABLE T encrypted=NO;
```

- table T의 암호화를 비활성화 시킵니다. 만약 전에 암호화가 되어있었다면 복호화합니다.

* 실적용 예 :

```
[mysqld]
plugin_dir=/usr/lib64/mysql/plugin/
plugin-load-add=file_key_management.so
file_key_management_encryption_algorithm=aes_cbc
file_key_management_filename = /var/lib/mysql/keys.enc
file_key_management_filekey = secret

innodb-encrypt-tables = ON
innodb-encrypt-log = 1
```

* so 파일은 /usr/lib64/mysql/plugin/ 에 위치 (centos 7.0 기준)

* 주의 : 테이블 암호화를 적용하면 DB 권한이 있는 유저로 접속했을때 암호화가 풀린상태로 보인다.( 실제로 달라진게 없는것처럼 보인다. 적용이 안된것처럼) 적용된 것을 확인하는 방법을 찾아보니

```
strings /var/lib/mysql/sample_table/user.ibd | grep "knownuser"
```

이러한 방법으로 확인할 수있다. 암호화가 적용되면 어떤한 데이터도 잡히지 않는다.

참고 : 
* [https://mariadb.com/kb/ko/data-at-rest-encryption/](https://mariadb.com/kb/ko/data-at-rest-encryption/)
* [http://stackoverflow.com/questions/33817877/verifying-mariadb-10-1-encryption](http://stackoverflow.com/questions/33817877/verifying-mariadb-10-1-encryption)
* [https://mariadb.com/kb/ko/encryption-plugins/](https://mariadb.com/kb/ko/encryption-plugins/)