---
title: "Base files of Vue"
excerpt: "About basic files of Vue"
excerpt_separator: "<!--more-->"
categories:
  - Vue.js
tags:
  - Vue.js
  - JavaScript
last_modified_at: 2021-02-02T09:10:00
---
<!--more-->

<br>

## Vue 생성 시 자동으로 포함되는 파일들

  * Vue 프로젝트를 구성하기 위해서 사용되는 각각의 라이브러리들이나 기능에 대한 설정 파일 
    * .browserslistrc
    * .eslintrc.js
    * .gitignore
    * babel.config.js
    * jest.config.js
  
  * package.json: 현재 패키지에서 사용하는 라이브러리를 관리하는 파일
  
  * public: 기본적인 html이 들어가는 디렉토리
  
  * src: Vue.js 기반으로 만들어진 항목들이나 관련된 리소스들이 위차하는 디렉토리
  
    * assets: css 같은 스타일 문서나 그림, 폰트 등의 구성이 들어가는 디렉토리
    * components: url 중 재사용성 있는 부분을 따로 구성한 파일을 모아놓는 디렉토리. 마치 java의 클래스와 같은 역할을 하는 파일들이 모여있다고 생각하면 됨.
    * router: 각 url을 어떤 페이지와 연동할 것인지 설정하는 곳
    * store: Component 개념이 기본적으로 트리구조로 이루어져 있는데, 이에 따라 수많은 연결관계를 가진 파일들 사이의 Data Share에 대한 문제가 발생. 이를 해결하기 위해 도출된 개념이 store로서, CUD는 어렵게 하여 데이터의 손실을 방지하는 동시에 R을 쉽게 하여 다양한 파일들이 데이터를 쉽게 공유할 수 있도록 하였다.
    * views: 페이지들의 디렉토리. 각각의 url들과 연동되는 페이지들이 이 곳에 있으며, 이 페이지들은 필요한 component를 가지고 와 사용하는 시스템.
  
  * tests: 단위 테스트를 위해 테스트 케이스 자동화를 위한 소스들이 들어있는 디렉토리
  
  * main.js: 가장 먼저 시작되는 자바스크립트 파일
  
  * App.vue: 가장 먼저 시작되는 Vue. main.js가 App.vue를 부르는 구조.
  
## Router

  * 페이지와 임의의 url을 연동하는 파일을 담고 있다.
  * 페이지 파일의 경우 두 가지 방법으로 넣는 것이 가능한데, 하나는 해당 페이지 파일을 import 하여 아래에서 사용하는 것이고, 또 하나는 아예 코드 내에서 import 하는 방식이다.
  * 페이지 파일을 명시할 때 component로서 명시하게 되는데, 이는 모든 페이지가 component 개념에 내포되어 있기 때문이다.
  * name은 Unique ID 라고 보면 되며, router는 이를 통해 url을 관리한다. 즉, name은 중복되어서는 안된다.
  * component를 명시할 때 Arrow Function으로 선언하게 되면 이는 비동기 방식으로 페이지를 불러오는 것이다. 본래 Vue.js는 SPA(Single Page Application)로서 하나의 페이지에서 모든 것을 처리하는 방식이다. 따라서 하나의 웹 사이트에 접속하면 모든 페이지를 전부 불러와야 하는 비효율을 야기하는데, 이를 방지하기 위한 방식으로 Arrow Function을 이용한 비동기 방식을 통하면 해당 url에 접속했을 때 해당 페이지를 로딩하게 된다.
  * .vue는 바로 웹서버에서 사용될 수 없다. Build가 된 후에야 html, .js가 되어 웹서버에 올라갈 수 있다. 'webpackChunkName'은 Build가 된 후에 묶이는 정적 파일의 이름을 명시하는 것이다. 