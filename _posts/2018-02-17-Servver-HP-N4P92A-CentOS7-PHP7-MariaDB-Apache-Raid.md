---
layout: post
title: "[Server] 3번째 N4P92A/CentOS7/PHP7/MariaDB10.1.17/Apache/ssh/vsftp/iptables/Raid구성"
`: Server
tags:
- 서버
- Server
- HP서버
- N4P92A
- CentOS
lastmod : 2018-02-17 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->

## UEFI모드에서  B140i 통한 RHEL7  설치 및 DD하기

## 1.  B140i DD Download

(드라이버는 주기적으로 업데이트 될 수 있으므로 그때그때 확인하시기 바랍니다.)

[참고](http://h20564.www2.hpe.com/hpsc/swd/public/detail?sp4ts.oid=7304563&swItemId=MTX_d21cf98caf904d8d91cb62ba46&swEnvOid=4176)


다운로드하신 드라이버 hpxxx.dd.gz  압축 풀면 hpxxx.dd 파일 확인되며, 확장자명에 .iso를 추가합니다.

```
예：hpdsa-1.2.6-115.rhel7u0.x86_64.dd.iso
```

해당 파일을 FAT32파일시스템인USB메모리에 복사합니다.

## 2.UEFI 설정항목

UEFI 모드 설정 및 UEFI Optimized Boot  Disabled 설정하기

![1.jpg]({{ site.baseurl }}/images/posts/2018-02-17-Servver-HP-N4P92A-CentOS7-PHP7-MariaDB-Apache-Raid/1.jpg)

Embedded SATA Configuration 에서 RAID 모드 설정 확인：

![2.jpg]({{ site.baseurl }}/images/posts/2018-02-17-Servver-HP-N4P92A-CentOS7-PHP7-MariaDB-Apache-Raid/2.jpg)

## 3. OS Install

Array 구성하고 OS 설치합니다.(F10 SSA에서 Array 설정)

OS 설치이미지 장치와 DD USB 메모리 모두 서버에 연결하고, OS 이미지로 부팅합니다

OS 설치화면으로 들어가기 전에 E키를 신속하게 눌러 편집모드로 진입.

![3.jpg]({{ site.baseurl }}/images/posts/2018-02-17-Servver-HP-N4P92A-CentOS7-PHP7-MariaDB-Apache-Raid/3.jpg)

편집모드에 들어가면 아래와 같습니다.

![4.jpg]({{ site.baseurl }}/images/posts/2018-02-17-Servver-HP-N4P92A-CentOS7-PHP7-MariaDB-Apache-Raid/4.jpg)

커서를 ”linuxefi” 라인 뒤에 옮기고, 아래 값을 입력합니다.

```
modprobe.blacklist=ahci inst.dd
```

입력하고  Ctrl+X 누르면 로딩 시작합니다.

![5.jpg]({{ site.baseurl }}/images/posts/2018-02-17-Servver-HP-N4P92A-CentOS7-PHP7-MariaDB-Apache-Raid/5.jpg)

일정시간 로딩 후 아래 화면이 나타납니다：

> 목록이 나오지 않았을경우 R키 입력하여 새로고침을 하면 목록이 갱신된다.

USB 메모리 장치 번호를 확인하고, 대응된 번호를 입력 후 Enter：

![6.jpg]({{ site.baseurl }}/images/posts/2018-02-17-Servver-HP-N4P92A-CentOS7-PHP7-MariaDB-Apache-Raid/6.jpg)


dd.iso 파일 대응된 번호 입력 후 Enter：

![7.jpg]({{ site.baseurl }}/images/posts/2018-02-17-Servver-HP-N4P92A-CentOS7-PHP7-MariaDB-Apache-Raid/7.jpg)

대응된 드라이버 번호 입력 후 Enter：

 ![8.jpg]({{ site.baseurl }}/images/posts/2018-02-17-Servver-HP-N4P92A-CentOS7-PHP7-MariaDB-Apache-Raid/8.jpg)

C키 입력 후 계속：

> 레이드 드라이버 dd파일 모두를 등록하여야 한다. 위에 작업 반복

![9.jpg]({{ site.baseurl }}/images/posts/2018-02-17-Servver-HP-N4P92A-CentOS7-PHP7-MariaDB-Apache-Raid/9.jpg)

드라이버 업로드 완료 후, C키 입력하고 계속：

![10.jpg]({{ site.baseurl }}/images/posts/2018-02-17-Servver-HP-N4P92A-CentOS7-PHP7-MariaDB-Apache-Raid/10.jpg)

커널 로딩 진행：

![11.jpg]({{ site.baseurl }}/images/posts/2018-02-17-Servver-HP-N4P92A-CentOS7-PHP7-MariaDB-Apache-Raid/11.jpg)

언어 선택하는 화면이 나오고 OS 설치 위한 각 설정 및 설치 하시면 됩니다

![12.jpg]({{ site.baseurl }}/images/posts/2018-02-17-Servver-HP-N4P92A-CentOS7-PHP7-MariaDB-Apache-Raid/12.jpg)

레이드 드라이버가 정상적으로 올라갔다면 파티션 화면에서 하드디스크가 로지컬 볼륨으로 화면에 출력될것이다(dd파일 모두 적용 – 리소스)

---

OS 설치 후 ->

초기 설정

- 패키지 최신 버전 업데이트

```
# yum update -y

# ip addr (ip주소 확인)
```

- ssh 설치

```
# yum -y install openssh-server openssh-client openssh-askpass

# rpm -qa | grep ssh (설치 확인)
```

- ssh 포트 변경 및 설정

```
# vi /etc/ssh/sshd_config

  #Port 22 <== 주석 처리되어있는 부분을 삭제하고 원하는 포트번호 입력

  #PermitRootLogin yes <== no로 변경하여 root 로그인 차단

# vi /etc/sysconfig/iptables
  -A INPUT -p tcp -m state --state NEW -m tcp --dport 포트번호 -j ACCEPT <== 방화벽 설정
```

참고 : [http://d4emon.tistory.com/58](http://d4emon.tistory.com/58)

---

- ssh 실행

```
# service sshd start

# service sshd status (실행 확인)
```

> sshd.service.failed 라고 뜰시 아래 확인

- 포트 열기

  만약 기본 포트 22 에서 변경을 했다면 sshd 서비스가 실행이 되지않을것이다.

  ss -nalt 로 확인해보면 바꾼 포트가 등록이 안돼있을것이다.(SELinux 보안요소떄문)

```
# yum install policycoreutils-python (semanage 명령을 실행하기 위한 툴 설치)

# semanage port -l | grep ssh

ssh_port_t     TCP      22
```
  위와 같이 나올것이다

```
# semanage port -a -t ssh_port_t -p tcp 22(원하는 포트번호)

# service sshd restart (ssh 재실행)

# ss -nalt (포트 확인)
```

참고 : [http://blog.elmitash.com/133](http://blog.elmitash.com/133)

---

- FTP 서버 설치

```
# yum -y install vsftpd ( vsftpd 설치 )

# systemctl enable vsftpd.service ( 부팅시 vsftpd 자동시작 )

# systemctl start vsftpd ( ftp 서비스 시작 )
```

- 방화벽 설치

```
# yum -y install system-config-firewall-tui
```

- 방화벽 허용 포트 설정

```
# vi /etc/sysconfig/iptables

-A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT ( 아파치 )

-A INPUT -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT ( SSH )

-A INPUT -p tcp -m state --state NEW -m tcp --dport 21 -j ACCEPT ( FTP )

-A INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT ( DB )
```
  위 내용 추가

- 방화벽 부팅시 자동시작 설정

```
# systemctl start iptables ( 방화벽 시작 )

# systemctl enable iptables.service ( 부팅시 자동 시작 )
```

- 아파치 서버 설치

```
# yum -y install httpd ( 아파치 설치 )

# systemctl enable httpd.service ( 부팅시 자동 시작 )

# systemctl start httpd ( 아파치 서버 시작 )
```

* 브라우저에서 작동 확인

참고 : [https://opentutorials.org/module/1701/10228](https://opentutorials.org/module/1701/10228)

---

- MariaDB 설치

```
# vi /etc/yum.repos.d/MariaDB.repo ( repo 파일 생성후 )

[mariadb]

name = MariaDB

baseurl = http://yum.mariadb.org/10.1/centos7-amd64

gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB

gpgcheck=1
```
  위와 같이 입력한후 저장

```
# yum install MariaDB-server MariaDB-client ( MariaDB 설치)
```

참고 : [https://mariadb.com/kb/en/mariadb/yum/](https://mariadb.com/kb/en/mariadb/yum/)

---

- 인코딩 latin1 -> utf8 로 바꾸기

```
# mysql (mysql 시작)

MariaDB[(none)]l> status ( 상태 확인)

--------------

mysql  Ver 15.1 Distrib 10.1.17-MariaDB, for Linux (x86_64) using readline 5.1

Connection id:          2

Current database:

Current user:           root@localhost

SSL:                    Not in use

Current pager:          stdout

Using outfile:          ''

Using delimiter:        ;

Server:                 MariaDB

Server version:         10.1.17-MariaDB MariaDB Server

Protocol version:       10

Connection:             Localhost via UNIX socket

Server characterset:    latin1

Db     characterset:    latin1

Client characterset:    utf8

Conn.  characterset:    utf8

UNIX socket:            /var/lib/mysql/mysql.sock

Uptime:                 5 sec


Threads: 1  Questions: 4  Slow queries: 0  Opens: 18  Flush tables: 1  Open tables: 11  Queries per second avg: 0.800

--------------
```
  위와같이 나오며 latin1 으로 설정되어있다.

```
# vi /etc/my.cnf.d/server.cnf

[mariadb]

* 위 항목밑에 character_set_server=utf8 내용 추가
```

- MariaDB 계정 및 데이터 베이스 생성,설정

```
# mysql

MariaDB [(none)]> create user '계정'@'%' identified by '비밀번호' ; ( 계정 생성 및 비번 설정)

MariaDB [(none)]> grant all privileges on * . * to '계정'@'%' identified by '비밀번호' with grant option; ( 계정 권한설정)

MariaDB [(none)]>  flush privileges;

MariaDB [(none)]> CREATE DATABASE `데이터베이스이름` /*!40100 COLLATE 'utf8_general_ci' */ ( 데이터베이스 만들기 )
```

- MariaDB port 변경

```
# vi /etc/my.cnf.d/server.cnf

[mysqld]

port = 설정포트번호 
```

  위와 같이 설정한다.

참고 : [http://sharadchhetri.com/2013/11/25/change-mysql-default-port-number-in-linux/](http://sharadchhetri.com/2013/11/25/change-mysql-default-port-number-in-linux/)

---

- php7 설치

```
# rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

# rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
```

* YUM 저장소 추가

```
# yum install php70w

# yum search php70w ( 설치할수 있는 모듈 리스트를 볼수있다.)

# yum install php70w-필요 모듈 (mcrypt,mysql,pdo,mbstring 등등)
```

참고 : [https://webtatic.com/packages/php70/](https://webtatic.com/packages/php70/)

---

- 패키지 최신 버전 업데이트

```
# yum update -y
```

- 심볼릭 설정

```
#  ln -s /지정폴더 ./심볼릭이름 ( 심볼릭 생성)
```

* PHP Warning:  Unknown: failed to open stream: Permission denied in Unknown on line 0 란 500에러가 뜬다면

```
# setsebool -P httpd_enable_homedirs 1

# chcon -R -t httpd_sys_content_t /보안미적용폴더
```

  위와 같이 하면 접속 되는걸 확인할수 있다.

참고 : 

[https://www.centos.org/forums/viewtopic.php?t=1742](https://www.centos.org/forums/viewtopic.php?t=1742)

[http://luckyyowu.tistory.com/139](http://luckyyowu.tistory.com/139)
