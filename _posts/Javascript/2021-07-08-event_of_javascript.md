---
title: "Event of Javascript"
excerpt: "Events of Javascript and How To Use Them"
excerpt_separator: "<!--more-->"
categories:
  - JavaScript
tags:
  - Event
last_modified_at: 2021-07-08T18:28:00
---

<!--more-->

<br>

## DOM(Document Object Model)

- DOM(Document Object Model): 자바스크립트 입장에서 웹문서를 객체 형태로 다루는 모델. 이를 통해 HTML 문서와 CSS 변경 가능.
- 하나의 태그 요소는 DOM 내 하나의 객체로 표현됨.
- DOM 접근은 getElementById() 메소드를 통해 가능.

## 이벤트 처리

- 이벤트 처리 방법
  1. 처리할 이벤트 선정
  2. 이벤트 핸들러 코드 작성
  3. 이벤트 등록

## 이벤트 종류

- 마우스 이벤트

  1. onclick: HTML 문서 내의 요소를 클릭했을 때 발생
  2. ondblclick: HTML 문서 내의 요소를 더블 클릭했을 때 발생
  3. onmousedown: 마우스 커서를 HTML 문서 내의 요소 위에 위치시키고 마우스 버튼을 누르는 순간 발생
  4. onmousemove: 마우스 커서를 HTML 문서 내의 요소 위에서 이동시킬 때 발생. 움직이는 동안에는 반복적으로 발생
  5. onmouseup: 마우스 커서를 HTML 문서 내의 요소 위에 위치시키고 마우스 버튼을 뗄 때 발생
  6. onmouseover: 마우스 커서가 해당 요소 위에 위치할 경우에 발생(1회 발생)
  7. onmouseout: 마우스 커서가 해당 요소 위를 벗어날 때 발생

- 키보드 이벤트

  1. onkeypress: 키보드를 누를 때 1회 발생하고 손을 떼기 전까지 계속 이벤트 발생
  2. onkeydown: 키보드를 눌러서 내려갈 때 1회 발생
  3. onkeyup: 키보드에서 손을 뗴어 버튼이 올라올 때 1회 발생

- 프레임/객체 이벤트

  1. onload: 문서, 프레임, 객체 등이 웹 브라우저 상에 로드가 완료되었을 때 발생하는 이벤트
  2. onresize: 문서 창, 문서 뷰의 크기가 리사이즈 되었을 때 발생
  3. onscroll: 문서 창, 문서 뷰가 스크롤되었을 경우 발생

- 폼 이벤트
  1. onchange: input, selection, textarea 등 폼 요소 콘텐츠의 내용이 변경되었을 때 발생하는 이벤트
  2. onfocus: 요소가 포커스 되었을 때 발생하는 이벤트. 마우스 클릭, 입력 커서 위치 등으로 발생
  3. onblur: focus가 없어질 때 발생
  4. onselect: input과 textarea 요소 내의 텍스트의 일부 혹은 전부가 선택되었을 때 발생

## 이벤트 핸들링 및 등록

- 이벤트 핸들러: 이벤트 발생 시 실행하고자 하는 자바스크립트 함수나 코드
- 이벤트 등록: 이벤트의 종류와 이를 처리할 이벤트 핸들러를 연결시키는 작업. 자바스크립트의 getElementById를 통해 객체를 지정하여 연결

## 폼 다루기와 이벤트 처리

- DOM 인터페이스로 input 요소에 접근하여 value 속성값을 수정<br>ex) document.getElementById("id1").value = 2;

## 동적 스타일 변경

- 보이기 스타일 속성 변경<br>ex) document.getElementById("id").style.visibility = "hidden";
- 배경색 스타일 속성 변경<br>ex) document.getElementById("id").style.background = "red";
- 위치 스타일 속성 변경<br>ex) document.getElementById("id").style.top = "2px";
- 마우스 포인터의 위치<br>ex) window.event.clientX // window.event.clientY

## 요소의 콘텐츠 변경을 통한 동적 문서

- innerHTML: 속성에 저장된 값을 HTML 태그로 해석
- innerText: 속성에 저장된 값을 단순히 문자열로 해석

## 폼 제어하기

- 아래 메소드들은 onclick과 같은 부분에 넣어 사용 가능하다.
  - select() 메소드
  - submit() 메소드
  - reset() 메소드
  - checked 속성 설정
