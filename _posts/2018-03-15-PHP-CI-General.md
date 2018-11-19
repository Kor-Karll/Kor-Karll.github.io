---
layout: post
title: "[PHP] CodeIgniter 보안"
category: PHP
tags:
- PHP
- CodeIgniter
- CI
- Session
- CSRF
- XSS

lastmod : 2018-03-15 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

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

    - config.php 설정 변경

    ```PHP
    ../application/config/config.php
    $config['csrf_protection'] = TRUE
    # 사용함으로 바꿈
    $config['csrf_token_name'] = 'csrf_token';
    # csrf 토큰 이름을 지정한다
    ```

    - 컨트롤러 및 뷰
    
    ```PHP
    // 컨트롤러
    function __construct()
    {
        parent::__construct();
        $this->load->helper('form');
        # form 헬퍼를 로드한다
    }

    // 뷰
    <?php
        $attr = Array('class' => 'form-horizontal', 'id' => 'test_write');
        echo form_open('test/write');
        # 위와같이 from_open 함수를 쓰면
        # <form class='form-horizontal' id='test_write' action=''>
        #   <input type='hidden' name='csrf_token value='7b806c7db763cf0d95018b99e855a8ad'>
        # 를 리턴 한다
    ?>
    <fieldset>
        <legend>테스트</legend>
        <div class='control-group'>
            <label class='control-label' for='test_input'>입력값</label>
            <div class='controls'>
                <input type='text' id='test_input'>
            </div>
        </div>     
    ```

    - form_open을 사용하지 않을경우
    ```PHP
        $data['csrf_token'] = $this->security->get_csrf_hash();
        $this->load->view('test/write', $data);
        # get_csrf_hash 함수를 사용하여 csrf_token 값을 받아오고
        # 뷰 영역으로 데이터를 넘겨 처리할수 있다
    ```



