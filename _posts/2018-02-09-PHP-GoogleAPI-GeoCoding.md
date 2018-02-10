---
layout: post
title: "[PHP] Google Map API GeoCoding 사용하기"
category: Django
tags:
- PHP
- GoogleAPI
- GeoCoding
- 위도,경도
- CURL
lastmod : 2018-02-09 17:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

# 조건
- 맵은 표시하지 않는다
- 주소를 Web에서 입력받는다
- 서버단에서만 주소를 통해 위도,경도,장소ID를 읽어온다

<!--미리보기-->

맵을 표시하지 않고 지오코딩 서비스만 이용하지만 지오코딩이 
[Node.js Client for Google Maps Services](https://developers.google.com/maps/web-services/client-library) 에서 제공 하므로 API 사용 등록을 해야한다.

[Google Developer 사이트](https://developers.google.com/maps/documentation/javascript/) 접속하여 키를 만든다

# 요청 형식

```php
{
 address: string,
 location: LatLng,
 placeId: string,
 bounds: LatLngBounds,
 componentRestrictions: GeocoderComponentRestrictions,
 region: string
}
```

필수 매개변수: 다음 필드 중 오직 하나만 제공해야 합니다.

* address — 지오코딩하려는 주소.

* location — 사람이 읽을 수 있는 가장 가까운 주소를 가져오려는 LatLng(또는 LatLngLiteral). 지오코더가 역지오코딩을 수행합니다. 자세한 내용은 [역지오코딩](https://developers.google.com/maps/documentation/javascript/geocoding#ReverseGeocoding)을 참조하세요.

* placeId — 사람이 읽을 수 있는 가장 가까운 주소를 가져오려는 장소의 ID. 장소 ID는 다른 Google API에 사용할 수 있는 고유 식별자입니다. 예를 들어, [Google Maps Roads API](https://developers.google.com/maps/documentation/roads/snap)에 의해 반환되는 placeId를 사용하면 스냅된 지점의 주소를 가져올 수 있습니다. 장소 ID에 대한 자세한 내용은 [장소 ID 개요](https://developers.google.com/places/place-id)를 참조하세요. placeId를 전달하면 지오코더가 역지오코딩을 수행합니다. 자세한 내용은 [역지오코딩](https://developers.google.com/maps/documentation/javascript/geocoding#ReverseGeocoding)을 참조하세요.

> 더 자세한 설명은 [Google Maps API](https://developers.google.com/maps/documentation/javascript/geocoding) 에서 확인

주소를 웹에서 입력받아

# 서버

```php
// Google Map API 로 GeoCoding( 주소를 통해 경도위도 읽어오기 )
function getGeoInfo_GoogleMap($address){
    $url = 'https://maps.googleapis.com/maps/api/geocode/json?address='.urlencode($address).'&key='.GOOGLE_API_MAPGEOCODING_KEY;

    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_POST, false);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt ($ch, CURLOPT_SSL_VERIFYHOST, 0);
    curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
    $result = curl_exec($ch);
    if ($result === FALSE) {
        error_log('Curl failed');
        die('Curl failed: ' . curl_error($ch));
    }
    curl_close($ch);
    return $result;
}
```

위와 같이 CURL GET 통신을 하는 방식으로 구현하였다.

$address 부분은 만약 띄어쓰기가 있다면 + 로 연결되는 형식을 써야하므로 urlencode 함수를 사용하였다.