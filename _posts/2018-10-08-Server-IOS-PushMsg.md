---
layout: post
title: "[Server]IOS APNS 메시지 보내기를 위한 서버세팅"
category: Server
tags:
- CentOS
- APNS
- IOS
- Push
- PHP
lastmod : 2018-10-08 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

미리보기

<!--미리보기-->

IOS 푸시메시지용 인증서(apns-dev-cert.p12)와 키(apns-dev-key.p12) 두개의 파일을 생성한 뒤 서버에 저장합니다

아래 와 같은 명령을 사용하여 PEM 파일 생성
```
openssl pkcs12 -clcerts -nokeys -out apns-dev-cert.pem -in apns-dev-cert.p12

openssl pkcs12 -nocerts -out apns-dev-key.pem -in apns-dev-key.p12
```

passphrease를 개인키에서 제거

```
openssl rsa -in apns-dev-key.pem -out apns-dev-key-noenc.pem
```

key파일과 cert파일을 통합 (이 파일로 APNS에 접근)

```
cat apns-dev-cert.pem apns-dev-key-noenc.pem > apns-dev.pem
```

PHP 코드

```
function iOS($message, $devicetoken) {
    $deviceToken = $devicetoken;
    $ctx = stream_context_create();
    // ck.pem is your certificate file
    stream_context_set_option($ctx, 'ssl', 'local_cert', PEM파일경로);
    stream_context_set_option($ctx, 'ssl', 'passphrase', 비밀번호);
    // Open a connection to the APNS server
    $fp = stream_socket_client(
        'ssl://gateway.push.apple.com:2195',$err,$errstr,60,STREAM_CLIENT_CONNECT|STREAM_CLIENT_PERSISTENT, $ctx);
    if (!$fp)
    {
        exit("Failed to connect: $err $errstr" . PHP_EOL);
    }

    // Create the payload body
    $body['aps'] = array(
        'alert' => array(
            'title' => $message['title'],
            'body' => $message['body'],
        ),
        'sound' => 'default'
    );
    // Encode the payload as JSON
    $payload = json_encode($body);
    // Build the binary notification
    $msg = chr(0) . pack('n', 32) . pack('H*', $deviceToken) . pack('n', strlen($payload)) . $payload;
    // Send it to the server
    $result = fwrite($fp, $msg, strlen($msg));

    // Close the connection to the server
    fclose($fp);
    if (!$result)
        return 'Message not delivered' . PHP_EOL;
    else
        return 'Message successfully delivered' . PHP_EOL;
}
```

APNS Host주소
개발용 : gateway.sandbox.push.apple.com
배포용 : gateway.push.apple.com
포트   : 2195 동일

참고 : http://theeye.pe.kr/archives/1454
      http://wonzopein.com/34