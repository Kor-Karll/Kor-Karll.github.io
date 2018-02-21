---
layout: post
title: "[Server] Jmeter 지표 보기"
category: Server
tags:
- Server
- Jmeter
- 테스트
- 서버테스트
lastmod : 2018-02-20 16:10:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

- Graph Results

 Graph Result는 모든 샘플 시간 동안 수행한 결과를 그래프로 보여 준다. Graph Result 그래프는 요청에 대한 응답 시간의 분포와 최고 응답 지연 시간(가장 늦은 응답 시간), 응답 시간의 평균, 표준 편차를 보여 준다

<!--미리보기-->

| 그래프 | 설명 |
| Data (검정) |  한 건의 요청 |
| Average (파랑) | Data 결과의 평균 |
| Median (보라) | Data 결과의 최소, 최대의 중간 값 |
| Throughput (초록) |  누적 요청 건수 |
| 세로축 | 응답 시간 |
| 가로축 | Sample 번호 |

Data는 그래프에서 검정색 점들이다. 각 샘플들의 응답 시간을 점으로 표시한다. 세로축의 맨 위 시간은 최고 응답 시간으로 가장 늦은 응답 시간을 말한다.

- Summary Report

Summary Report에서는 진행했던 테스트에 대한 결과를 한눈에 알 수 있게 표 형식으로 보여줍 니다. 최고, 최저 응답 지연 시간과 표준 편차, 누적 요청 건수 등을 알 수 있다.

![0.jpg]({{ site.baseurl }}/images/posts/2018-02-20-Server-Jmeter-Test/0.jpg)


```
 참고 : 에러가 없는데도 Error 의 Total 값이 0이 아닌 경우 

 테스트 과정에서 에러가 없음에도 불구하고 Error의 Total 값이 0이 아닌 경우가 있을 수 있다. View Result in Table 을 봤을 때 Sample 1번이 Error 로 돼있을 것 이다. 테스트를 완료하고 다시 테스트를 진행하고자 하는 경우 상단 메뉴 Run -> Clear All 을 통해 결과 값을 깨끗이 지우시기 바란다.
 ```

출처 : [http://www.slideshare.net/xenonix/apache-jmeter-41356991?from_action=save](http://www.slideshare.net/xenonix/apache-jmeter-41356991?from_action=save)