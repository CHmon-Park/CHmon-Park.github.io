---
title: "Micro Frontend"
excerpt: "Definition of Micro Frontend"
excerpt_separator: "<!--more-->"
categories:
  - ETC
tags:
  - Micro Frontend
last_modified_at: 2021-02-16T09:00:00
---
<!--more-->

<br>

### 현재까지의 프론트엔드 개발 한계

  * 고전적인 웹 프론트엔드 개발 방식은 모놀리틱 프론트엔드(Monolithic Frontend)라고 하여, 통일된 프레임워크 내에서 모두가 한번에 협업하는 형식이었다. 이는 해당 기술을 가지고 있는 인원에 한해 관리 및 유지보수 면에서 유리함을 가질 수 있기에 좋은 평을 받기는 했으나, 다른 면에서는  하나의 프레임워크에서 동일한 문법과 사용법만으로 개발된 것만이 실행될 수 있는 환경이었기에 불가피한 것이었다. 
  * 즉, 개발을 시작하고 기획함에 있어서 가장 우선시되어야 하는 것이 팀원들 사이의 소통 및 개발 능력의 통일이었으며, 이는 곧 팀원의 추가가 효율로 직결되지 않는 동시에, 다른 기술들과의 협업 및 조화가 제한적이라는 것을 의미했다.  
  
<br>

## Micro Frontend

### 정의 및 개념

  * Micro Frontend는 지금까지의 프론트 엔드 개발 방법을 효율적으로 분리하면서도 획기적으로 통합시키기 위한 개념이다. 
  * 지금까지는 하나의 페이지를 구성하기 위해 각 Component들이 한번에 구현되어야 했지만, Micro Frontend는 구분된 각 Component들의 개발을 완전한 독립 과정으로서 취급한다. 
  * 전체적인 프론트 엔드 구성 중 가장 유기적으로 뭉쳐야 하는 Component들을 구분하고, 나눠진 각 부분들은 개별적으로 기획, 개발, 유지 보수를 진행하게 된다. 이 때 필요로 하는 기술이나 약속 등도 Component별로 상이하게 할 수 있다. 
  * 최종적으로 각 부분들을 통합하는 Container Application이 존재하기에 Component별로 진행상황에 따라 유기적으로 업데이트하여 최종 결과물을 구현하게 된다.
  
### Components 통합 방법

1. Server-side template composition
  * 유저가 웹 페이지를 요청하면 Container app server가 연관된 html component server들에 해당 부분을 요청하고, 그것들을 조합하여 유저에게 Response 하는 방식이다.
  * 단순하고 비교적 직관적이라는 장점이 있다.
2. Build-time integration
  * Micro Frontend를 이루기 위해 Container Application이 Package 형태로 Component들을 라이브러리로서 사용하는 형태이다.
  * 이 방식의 경우 build 시 마다 Package를 Load하게 된다. 때문에 Frontend의 일부분만 바뀌어도 새로 build를 하게 되어 비효율을 초래한다. 
3. Run-time integration via iframes
  * iframe 태그를 이용하여 각 Component들의 route를 통해 html을 불러오는 형식이다.
  * iframe만 사용하면 되므로 간단하다는 장점이 있으나, 통합에서의 유연함과 반응성에 있어서는 다소 뒤처진다는 단점이 있다.
4. Run-time integration via JavaScript
  * JavaScript의 script 태그에서 원하는 Component들이 언제 어디에 출력되도록 할지 결정하는 형식이다.
  * Build-time integration 방식과는 달리 각기 다른 js 파일들을 독립적으로 배치가 가능하며, iframes 방식과는 달리 build 과정에서 충분한 유연성을 지닌다.
5. Run-time integration via Web Components
  * Run-time integration via JavaScript 방식과 결과는 비슷하나, Container가 global function을 통해 Micro Frontend를 새로이 정의할 수 있다는 점에서 차이가 있다.
  * global function의 경우 browser가 지원하는 기능에 따라 차이가 생긴다.
  
### 유의사항

  * UI 스타일 일관성은 UI Component Library를 만들어 통일성을 갖춘다.
  * 구분된 어플리케이션 사이의 통신은 Custom events를 사용한다.

### 장점 및 단점

#### pros

1. 각 Component별로 최적화가 가능하다.
2. 각 Component별로 저촉되는 부분이 거의 없기에 개별적으로 프론트 엔드 업그레이드가 가능하다.
3. 각 Component별로 대응해야 하는 사용자의 Needs를 분석하여 적용할 수 있다.
4. 각 Component별로 전용 DB, API, 백엔드 코드를 가질 수 있다.
5. 각 Component에 어울리는 팀원을 추가하면 프로젝트 진척 효율을 금세 높일 수 있다.
6. 각 Component별로 가지는 장점을 하나의 웹 페이지가 모두 흡수할 수 있다.

#### cons

1. 개발 환경이 Component마다 다르다보니 프로젝트 복잡도가 확연히 올라간다.
2. 중복되는 데이터의 정리가 충분히 되지 못하면 배포 번들 사이즈가 불필요하게 커질 수 있다.
3. 전체적인 프로젝트 운영이 복잡해진다.
4. 프로젝트를 시작하기 위한 준비 과정에서 비용이 많이 든다.

### 향후 가능성

  * Micro Frontend 아이디어는 다수의 인원이 참여하는 큰 규모의 프로젝트에 적합하며, 개발자 간 발생할 수 밖에 없는 개발 환경 차이의 간극을 획기적으로 좁힐 수 있다.
  * Micro Frontend를 적용하면 여러 Framework들이나 Library들이 한 번에 통합되기에, Monolithic 웹 페이지가 가진 한계가 사실상 사라진다고 할 수 있다.
  * 기업들 사이의 협력 과정, SI(System Integration) 서비스 등에서도 보다 효율적인 기획 및 개발이 가능하다.
