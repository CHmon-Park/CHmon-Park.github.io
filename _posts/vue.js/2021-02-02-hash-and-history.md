---
title: "Hash mode and History mode"
excerpt: "Difference between hash mode and history mode in Vue Router"
excerpt_separator: "<!--more-->"
categories:
  - Vue.js
tags:
  - Vue.js
  - JavaScript
  - Hash Mode
  - History Mode
last_modified_at: 2021-02-02T10:10:00
---
<!--more-->

<br>

## 해시 모드

  * SPA(Single Page Application)는 본래 Subpath의 개념이 없다. 즉, 웹 서버 상의 하위 디렉토리에 들어가는 방식은 없다. 대신 #을 이용하여 페이지를 찾아 들어갔다. # 뒤에 붙은 경로는 페이지 내부의 이름으로 여겨지기에 페이지가 다시 로드되지 않는다.
  * 그러나, 이 방식은 url을 가독성이 떨어지게 만든다는 단점이 있다. 이를 보완하기 위해 나온 방식이 history 모드이다.
  
## 히스토리 모드

  * 히스토리 모드는 단순히 '/'로 웹의 url을 구분 및 명시한다.
  * 히스토리 모드를 사용하기 위해서는 웹 서버에 어떤 url이 오더라도 index.html(root)로 보내라는 설정이 필요하다. 
  * 이후 index.html이 해당 url을 읽고 뒤의 값을 추출하여 해당 페이지를 로드하게 된다.
  * 히스토리 모드의 경우 요청한 url의 리소스가 없다면 반환하지 못하므로 404 페이지를 띄우기도 한다.