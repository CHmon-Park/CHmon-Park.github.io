---
title: "Restful API"
excerpt: "Kinds of Restful API, and what they mean"
excerpt_separator: "<!--more-->"
categories:
  - ETC
tags:
  - Restful API
  - Server
  - Network
last_modified_at: 2021-02-13T14:40:00
---
<!--more-->

<br>

## RESTful API

#### RESTful API란?

  * REST란 Representational State Transfer의 약자이다.
  * API(Application Programming Interface)는 Application Software를 구축하고 통합하는 정의 및 프로토콜 세트이다.
  * 즉, REST API는 REST 아키텍처의 제약 조건하에 있는 애플리케이션 프로그래밍 인터페이스를 의미한다.
  * RESTful API를 통해 요청이 수행되면 RESTful API는 리소스 상태에 대한 표현을 요청자에게 전송하는데, 이 때의 정보 혹은 표현은 HTTP: JSON(Javascript Object Notation), HTML, XLT 또는 일반 텍스트 형식이 될 수 있다. 이 중 JSON은 인간과 기계가 모두 읽을 수 있기에 가장 널리 사용되고 있다.
  
#### RESTful API의 기준(제약조건) 

  1. 인터페이스의 일관성: 
    * 요청된 리소스가 식별 가능해야 하며 클라이언트에 전송된 표현과 분리되어야 한다.
    * 수신한 표현을 통해 클라이언트가 리소스를 조작할 수 있어야 한다.
    * 클라이언트에 반환되는 자기 기술적(self-descriptive) 메시지에 클라이언트가 정보를 어떻게 처리해야 할지 설명하는 정보가 충분히 포함되어야 한다.
    * 클라이언트가 리소스에 액세스한 후 하이퍼링크를 사용해 현재 수행 가능한 기타 모든 작업을 찾을 수 있어야 한다.
  2. 무상태(Stateless): 각 요청 간 클라이언트의 콘텍스트가 서버에 저장되어서는 안된다.
  3. 캐시 처리 가능(Cacheable): www에서와 같이 클라이언트는 응답을 캐싱할 수 있어야 한다. -> 클라이언트-서버 간 상호작용을 부분적 혹은 완전히 제거하여 scalabiliy와 성능을 향상
  4. 계층화(Layered System): 중간 서버는 로드 밸런싱 기능이나 공유 캐시 기능을 제공함으로써 시스템 규모 확장성을 향상시키는데 유용하다.
  5. Code on demand: 자바 애플릿이나 자바스크릡트 제공을 통해 서버가 클라이언트가 실행시킬 수 있는 로직을 전송하여 기능을 확장시킬 수 있다.
  6. 클라이언트-서버 구조: 아키텍처를 단순화시키고 작은 단위로 분리함으로써 클라이언트-서버의 각 파트가 독립적으로 개선될 수 있도록 한다.
  
#### REST 구성

  * 자원(RESOURCE)
  * 행위(Verb)
  * 표현(Representations)
  
#### REST API 중심 규칙

  1. URI는 정보의 자원을 표현해야 한다.
    * 리소스명은 명사를 사용하는 것이 보다 타당하며, 행위에 대한 표현은 지양하는 것이 좋다.
  2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, PATCH, DELETE)로 표현한다.
  
**Put vs Patch**: Put이 리소스의 전체를 교체하는 한편, Patch는 리소스의 일부를 수정한다. 그렇기에 명령어를 사용할 때도 Put은 모든 데이터를 다 명시해야 하지만, Patch는 일부 데이터만 명시하여도 수정이 가능하다. 
{: .notice--info}