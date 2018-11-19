---
layout: post
title: nginx 주소창에서 확장자 처리
category: Server
tags:
- Server
- nginx
- PHP
- URL
lastmod : 2018-02-21 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

/etc/nginx/conf.d/도메인.cnf  를 수정한다.

<!--미리보기-->

```
location / {
    try_files $uri $uri.html $uri/ @extensionless-php;
    index index.html index.htm index.php;
}

location ~ \.php$ {
    try_files $uri =404;
}

location @extensionless-php {
    rewrite ^(.*)$ $1.php last;
}

```

위와 같이 수정하면 php를 생략해도 .php가 붙은거와 같이 작동한다.



참고 : [http://stackoverflow.com/questions/21911297/how-to-remove-both-php-and-html-extensions-from-url-using-nginx](http://stackoverflow.com/questions/21911297/how-to-remove-both-php-and-html-extensions-from-url-using-nginx)