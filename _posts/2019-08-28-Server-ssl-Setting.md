---
layout: post
title: "[Server] Nginx SSL 인증서 적용"
category: Server
tags:
- Server
- SSL
- 인증서적용
- Nginx

lastmod : 2019-08-28 15:00:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

<!--미리보기-->
### 1. 인증서 적용하기
- 메일의 첨부된 파일을 서버에 업로드 하여 파일 확인

```linux
# ls

AddTrustExternalCARoot.crt  COMODORSAAddTrustCA.crt rsa-dv.chain-bundle.pem _wildcard_.yourdomain.net.crt   _wildcard.yourdomin.net_SHA256WITHRSA.key
```

- cat 명령어를 이용하여 ' 도메인인증 - 체인인증서 - 루트인증서 ' 순서로 내용을 합침

```linux
# cat _wildcard_.yourdomain.net.crt rsa-dv.chain-bundle.pem AddTrustExternalCARoot.crt > yourdomin.net.crt
```

- nginx 설정파일 /etc/nginx/conf.d/https.conf 수정

```linux
server {

    add_header X-Frame-Options SAMEORIGIN;
    add_header X-Content-Type-Options nosniff;
    add_header X-XSS-Protection "1; mode=block";
    # add_header Cache-Control public;

    listen 443;
    ssl on;

    server_name yourdomin.net;

    ssl_certificate /opt/ssl/yourdomin.net.crt;
    ssl_certificate_key /opt/ssl/_wildcard.yourdomin.net_SHA256WITHRSA.key;

    #ssl_session_cache shared:SSL:1m;
    ssl_session_timeout  5m;

    ssl_ciphers  HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers   on;
    # ssl_protocols SSLv2 SSLv3 TLSv1.2 TLSv1.1 TLSv1;
    ssl_protocols SSLv2 TLSv1.2 TLSv1.1 TLSv1;

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm index.php;
    }

```

### 2. 웹서버 재실행

```linux
# service nginx restart
```

### 3. 웹서비스 동작상태 점검

- 인터넷 주소창에 https://사용도메인 입력후 해당 페이지 정상작동여부 확인

참고 : [Nginx : 인증서 적용 - HanbiroSSL](https://www.comodossl.co.kr/certificate/ssl-installation-guides/Nginx.aspx)