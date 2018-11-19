---
layout: post
title: "[MariaDB] 복제 Master-Slave 설정"
`: DB
tags:
- MariaDB
- 복제
- 백업
lastmod : 2018-03-13 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

## DB 복제 설정

<!--미리보기-->

[Master 서버]

- DB 설정 변경

```
vi /etc/my.cnf.d/server.cnf

[mysqld]
server-id        = 1
log_bin          = /var/log/mysql/mariadb-bin
log_bin_index    = /var/log/mysql/mariadb-bin.index
expire_logs_days = 10
max_binlog_size  = 100M
# /var/log/mysql 의 소유자는 mysql 이어야한다
```

- 설정 변경후 mysql 재시작

```
service mysql restart
```

- mysql 커맨드라인 클라이언트 실행 후
- 복제권한이 있는 replication_user 라는 계정생성

```
GRANT REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'replication_user'@'%' IDENTIFIED BY 'password';
```

- 운영중인 서버라면 DB에 락을 걸고 작업

```
FLUSH TABLES WITH READ LOCK;
SHOW MASTER STATUS;
# MASTER 정보 조회

+--------------------+----------+--------------+------------------+
| File               | Position | Binlog_Do_DB | Binlog_Ignore_DB |
+--------------------+----------+--------------+------------------+
| mariadb-bin.000001 |     2326 |              |                  |
+--------------------+----------+--------------+------------------+
# File 과 Position 기억 Slave 구성시 사용
```
[Slave 서버]

- DB 설정 변경

```
vi /etc/my.cnf.d/server.cnf

[mysqld]
server-id           = 2
log_bin             = /var/log/mysql/mariadb-bin
log_bin_index       = /var/log/mysql/mariadb-bin.index
expire_logs_days    = 10
max_binlog_size     = 100M
relay_log           = /var/log/mysql/relay-bin
relay_log_index     = /var/log/mysql/relay-bin.index
relay_log_info_file = /var/log/mysql/relay-bin.info
log_slave_updates
# 복제하지 않을 database 지정
replicate-ignore-db = test
replicate-ignore-db = information_schema
replicate-ignore-db = mysql
```

- 설정 변경후 mysql 재시작

```
service mysql restart
```

- mysql 커맨드라인 클라이언트 실행

```
CHANGE MASTER TO
MASTER_HOST='Master IP',
MASTER_USER='replication_user',
MASTER_PASSWORD='password',
MASTER_PORT=portNumber,
MASTER_LOG_FILE='Master File', # Master 정보에서 File 부분 입력
MASTER_LOG_POS=Master Position,# Master 정보에서 Position 부분 입력
MASTER_CONNECT_RETRY=10;
   
FLUSH PRIVILEGES;
  
START SLAVE;

```

- Slave 상태 확인

```
SHOW SLAVE STATUS\G; 

*************************** 1. row ***************************
               Slave_IO_State: Waiting for master to send event
                  Master_Host: 192.168.0.22
                  Master_User: replication_user
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: mariadb-bin.000001
          Read_Master_Log_Pos: 2326
               Relay_Log_File: relay-bin.000002
                Relay_Log_Pos: 896
        Relay_Master_Log_File: mariadb-bin.000001
             Slave_IO_Running: Yes  # Yes가 아니면 연결 실패
            Slave_SQL_Running: Yes  # Yes가 아니면 연결 실패
              Replicate_Do_DB: 
          Replicate_Ignore_DB: test,information_schema,mysql
           Replicate_Do_Table: 
       Replicate_Ignore_Table: 
      Replicate_Wild_Do_Table: 
  Replicate_Wild_Ignore_Table: 
                   Last_Errno: 0
                   Last_Error: 
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 2326
              Relay_Log_Space: 1199
              Until_Condition: None
               Until_Log_File: 
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File: 
           Master_SSL_CA_Path: 
              Master_SSL_Cert: 
            Master_SSL_Cipher: 
               Master_SSL_Key: 
        Seconds_Behind_Master: 0
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 0
                Last_IO_Error: 
               Last_SQL_Errno: 0
               Last_SQL_Error: 
  Replicate_Ignore_Server_Ids: 
             Master_Server_Id: 1
               Master_SSL_Crl: 
           Master_SSL_Crlpath: 
                   Using_Gtid: No
                  Gtid_IO_Pos: 
      Replicate_Do_Domain_Ids: 
  Replicate_Ignore_Domain_Ids: 
                Parallel_Mode: conservative
                    SQL_Delay: 0
          SQL_Remaining_Delay: NULL
      Slave_SQL_Running_State: Slave has read all relay log; waiting for the slave I/O thread to update it
1 row in set (0.00 sec)

ERROR: No query specified

```

- 위와 같이 나오면 연결 성공
- 성공 후 Master 서버 락 해제(락을 걸었을 경우)

---
## 주의 사항

- DB 변경사항이 log 파일로 저장된 후 Slave 서버에서 그 파일을 읽어들여 변경사항을 그대로 DB에 적용하는 방식이다
- 위와같은 이유로 기존 데이터가 있다면 Slave 서버에 복사한 후 진행해야한다.(기존데이터는 복제하지 않음)
- Slave 에서 제대로 연결이 되었다면 Master Position 번호와 파일을 자동으로 업데이트 한다.

### 참고
[http://hyeonil.blogspot.kr/2016/05/mariadb-replication.html](http://hyeonil.blogspot.kr/2016/05/mariadb-replication.html)
- 책 [MariaDB 구축과 활용](http://www.yes24.com/24/goods/22356573?scode=032&OzSrank=1)



