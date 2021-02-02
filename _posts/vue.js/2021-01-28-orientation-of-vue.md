---
title: "Orientation of Vue"
excerpt: "Basic knowledge of Vue / How to install it"
excerpt_separator: "<!--more-->"
categories:
  - Vue.js
tags:
  - Vue.js
  - JavaScript
  - VS Code
last_modified_at: 2021-01-28T10:40:00
---
<!--more-->

<br>

## Vue.js

  * Vue란 사용자 인터페이스를 만들기 위한 프로그레시브 프레임워크이다.
  * 다른 단일형 프레임워크와 달리 Vue는 점진적으로 채택할 수 있도록 설계되어 있다.
  * 핵심 라이브러리는 뷰 레이어만 초점을 맞추어 다른 라이브러리나 기존 프로젝트와의 통합이 매우 쉽다.
  
#### Vue 설치

  * 설치 항목
    * nodejs v14.x LTS
    * git, current version
    * visual studio code, current version
<br>
  * 설치 과정
    1. windows powershell 혹은 cmd 에서 자신이 원하는 경로에 도달한 뒤 아래의 명령어를 통해 Vue를 다운받는다. 명령어 중 '-g'는 global의 의미를 담고 있어 vue를 컴퓨터 전역에서 사용하도록 다운받는 것을 의미한다. 즉, 이 표현이 없을 경우 해당 경로에서만 Vue의 사용이 가능하다.
     
        npm install -g @vue/cli
        {: .notice--info}
    2. 폴더 경로에서 아래의 명령어를 이용하여 프로젝트를 생성한다.
    
        vue create my-project
        {: .notice--info}
        
    3. 설치 과정 중 Vue의 설정을 위해 preset이나 모듈 등을 customizing 하게 된다. 이 중 preset에서는 'Manually select features'를 선택한다.
    
    4. 선택하는 preset은 다음과 같다.
      * Babel
      * Router
      * Vuex
      * CSS Pre-processors
      * Linter / Formatter
      * Unit Testing
      
    5. history 모드를 설정하는 구간에서는 yes로 답한다. (history 모드에 대해서는 차후에 다시 기술하겠다. 참고로 해시모드와 비교된다.)
    
    6. CSS pre-processor 는 Sass/SCSS (with node-sass)로 선택한다.
    
    7. Linter / formatter config는 prettier이다.
    
    8. additional lint features는 Lint on save.
    
    9. unit testing solution 은 Jest.
    
    10. Babel 이나 ESLint 등의 config 위치는 Indedicated config files로.
    
    11. 이후 현재까지 지정한 preset을 프로젝트의 preset으로서 저장한다.
    
    12. 현재 생성된 프로젝트를 시험해보기 위해서는 커맨드 창에 아래와 같은 명령어를 통해 로컬 서버를 실행시킨다.
    
        npm run serve
        {: .notice--info}
    
#### VS Code 환경 설정

  * Vue를 설치한 뒤 프로젝트를 생성하고 나면 이후 과정은 VS Code에서 수정 및 진행이 가능하다.
  * 이를 위해서는 VS Code 자체에서 내재해야 할 설정, 모듈, 라이브러리 등이 있는데, 내용은 아래와 같다.
  
    1. 확장 탭에서 아래의 라이브러리들을 설치한다.
    
        material theme<br>
        material icon theme<br>
        prettier<br>
        bracket pair colorizer<br>
        indent-rainbow<br>
        auto rename tag<br>
        css peek<br>
        html css support<br>
        live server<br>
        html to css autocompletion<br>
        vue vscode snippets
        {: .notice--info}
        
    2. VS Code 의 default formatter를 prettier로 변경한다.
    
    3. 만약 VS Code에서 npm이 작동하지 않는다면 Windows Powersell 에서 이를 설정할 수 있다.
      * Windows Powershell 을 관리자 권한으로 실행.
      * 'get-help Set-ExecutionPolicy' 명령어를 통해 어떤 권한을 설정할 수 있는지 확인.
      * 'Set-ExecutionPolicy RemoteSigned' 명령어를 통해 권한 설정 변경.
      * 참고로 권한에는 다음과 같은 내용이 들어갈 수 있다.
      
        * Restricted: PowerShell의 실행 권한 정책 중 기본적으로 적용되어 있는 옵션으로, ps1 스크립트 파일을 로드하여 실행할 수 없는 정책.
        * AllSigned: 신뢰된 배포자에 의해 서명된 스크립트만 실행할 수 있는 정책.
        * RemoteSigned: 로컬 컴퓨터에서 본인이 생성한 스크립트만 실행 가능. 또는 인터넷에서 다운로드 받은 스크립트는 신뢰된 배포자에 의해 서명된 것만 실행 가능한 정책.
        * Unrestricted: 제한 없이 모든 스크립트를 실행 가능한 정책.
        * ByPass: 어떤 것도 차단하지 않고 경고 없이 실행 가능한 정책.
        * Undefined: 정책 적용 안함.
        
#### tailwind 설치

  * tailwind란 css 속성들을 모아놓은 파일로서, 보다 직관적인 네이밍과 속성값들로 css 적용을 편하게 해주는 도구라고 할 수 있다.
  * 설치과정은 다음과 같다.
    1. 'vue add tailwind' 라는 명령어를 통해 tailwind를 다운로드 받는다. 이 경우 vue 명령어를 사용해야 하기에 vue가 다운로드 되어 있어야 한다.
        
