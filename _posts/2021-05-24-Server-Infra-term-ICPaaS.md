---
layout: post
title: "IaaS CaaS PaaS"
category: Server
tags:
- Server
- IaaS
- CaaS
- PaaS
- 인프라용어

lastmod : 2021-05-24 15:00:00
sitemap :
  changefreq : daily
  priority : 1.0
---

***

## Iaas Caas Paas

<!--미리보기-->

### IaaS(Infrastructure as a Service)
- 가사 머신, 스토리지, 네트워크 같은 인프라를 필요한 만큼 적시에 제공하는 서비스로서 사용자는 이러한 인프라를 이용해 개발 환경을 구성한 후 애플리케이션을 배포한다. 가상 서버, 가상 네트워크, 가상 스토리지라 생각하면 이해하기 쉽다.
- 예) AWS EC2, GCP Compute Engine, Azure VM

### CaaS(Container as a Service)
- 컨테이너 기반 가상화를 사용해 컨테이너를 업로드, 구성, 실행, 확장, 중지할 수 있는 서비스다. 애플리케이션을 바로 구동할 수 있는 환경을 제공한다는 점에서 PaaS와 유사하지만 다른 환경에도 이식 가능한 컨테이너 기반 가상화를 제공한다는 점이 다르다.
- 예) Service(EKS), Google Kubernetes Engine(GKE), AWS ECS

### PaaS(Platform as a Service)
- 복잡함 없이 애플리케이션을 곧바로 개발, 실행, 관리할 수 있는 플랫폼 환경을 서비스 형태로 제공한다. IaaS 위에 실제로 애플리케이션이 실행될 수 있는 미들웨어나 런타임까지 탑재된 환경이라 생각하면 이해하기 쉽다.
- 예) Azure Web App, Google App Engine, Cloud Foundry, Heroku, AWS Elastic Beanstalk

참고 : 책 '도메인 주도 설계로 시작하는 마이크로서비스 개발' p35-36

