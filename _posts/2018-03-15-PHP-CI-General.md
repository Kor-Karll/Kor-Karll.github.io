---
layout: post
title: "[PHP] CodeIgniter 세션 및 보안"
category: PHP
tags:
- PHP
- CodeIgniter
- CI
- Session

lastmod : 2018-03-15 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***
오늘 알게된 CodeIgniter 내용들
<!--미리보기-->
### CI 에서 자체적으로 제공하는 보안 기능

* SQL 인젝션 방어

```PHP
1.  $sql = "SELECT * FROM TEST WHERE testid = '".$this->input->post('testid',TRUE)."'";

2.  $sql = "SELCT * FROM TEST WHERE testid = ?";
    $this->db->query($sql, Array($testid,));
# 위와 같이 바인딩 하는방법
3.  $this->db->where(Array('testid' => $this->input->post('testid',TRUE)));
    $this->db->get('TEST');
# CI 자체 함수를 이용하는 방법
```

* XSS 방어

```PHP
$_POST 함수로 직접 접근하지 않고

$this->input->post('testvalue', TRUE);

#위와 같이 사용하면 필터링을 한다.
```

* CSRF 방어

```PHP

```

작성중



