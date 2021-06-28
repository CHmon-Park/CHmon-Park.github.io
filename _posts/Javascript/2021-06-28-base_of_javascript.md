---
title: "Base of Javascipt"
excerpt: "Basic usage of Javascript"
excerpt_separator: "<!--more-->"
categories:
  - JavaScript
tags:
  - Basic
last_modified_at: 2021-06-28T14:42:00
---

<!--more-->

<br>

## Javascript 작성하기

- 자바스크립트는 html 파일 내에 포함되어야 하는데, 그 방식은 두 가지로 나뉜다.

  * 웹 문서 내장 방식: &lt;script&gt; 태그 안에 자바스크립트 코드 삽입
  * 외부 파일 참조 방식: &lt;script&gt; 태그 안에 src 속성 값으로 자바스크립트 파일의 파일 경로 또는 url 경로 지정

```javascript
<script type="text/javascript" src="http://webclass.me/html5/yourscript.js">
</script>
```

## Javascript 화면 출력

- HTML 문서는 Document라는 객체로 모델링되어 있다.
- Document 객체를 이용하여 document.write() 명령어를 사용하면 HTML 문서에 콘텐츠를 추가할 수 있다.

## Javascript 기본 변수

- 대부분의 자바스크립트 변수는 사용 전에 선언할 필요가 없으며, 타입도 지정할 필요가 없다. 대신 전역변수나 지역변수, 상수와 같은 것은 잘 적용시켜두는 것이 중요하다.
- 변수형은 typeof() 메소드를 사용하여 확인이 가능하다.
- 자료형 종류
  * Number: 정수, 실수 등 숫자값. Number 형은 내부적으로 모든 숫자를 실수로 저장. **만약 String 타입과 연산될 경우 자동으로 String으로 변환됨.**
  * String: 문자열
  * Boolean: true or false
  * Undefined: 값이 할당되지 않은 값
  * Null: 객체가 없는 객체 참조 시 발생

## Javascript 변수 선언

- 변수 이름은 대소문자를 구분함
- 사전에 선언하지 않고 변수 사용가능. 단, 전역 변수로 사용할 때는 미리 선언되어 있어야 함.
- 종류
  * let: 지역 변수
  * var: 전역 변수
  * const: 상수

## Javascript 기본 연산자

  * 사칙연산: +, -, *, /, %
  * 대입연산자: +=, -=, *=, /=, %=
  * 증감연산자: ++, --
  * 논리연산자: >, >=, <, <=, ==, !=, ===, !==, !, ||, &&
- ==: 값이 값다.<br>===: 값과 타입이 같다.
- 숫자와 문자열의 비교 시, 문자열이 숫자라면 숫자로 변환하여 비교하고, 그렇지 않으면 항상 false로 결과가 출력된다.

## 문자열 붙이기

- '+' 연산자를 이용해서 두 문자열을 붙이는 것이 가능함.
- 문자열과 숫자를 대상으로 하면 숫자를 문자열로 변환하여 붙임.

## 변수 형변환

- 문자열 타입 -> 숫자 타입
  * 문자열 변수를 parseInt() 또는 parseFloat() 함수에 입력
- 숫자 타입 -> 문자열 타입
  * 숫자 변수의 toString() 메소드 이용

## 입출력을 위한 대화상자

  * alert(): 대화상자로 메시지 출력. 사용자에게 경고사항이나 메시지를 전달. [확인] 버튼을 누를 때까지 자바스크립트 실행을 멈추고 대기함
  * confirm(): 확인 입력받기. [확인]을 누르면 true, [취소] 또는 창을 닫게 되면 false 반환
  * prompt(): 문자열 입력 받기. 대화상자에는 메시지와 초기 입력값이 표시. [확인]을 누르면 입력된 문자열, [취소]를 누르면 null 반환.<br>prompt("메시지", "초기값")

## Javascript 제어문

  * if- else if-else
```javascript
if(a == b) {
  return b
} else if (a == c) {
  return c
} else {
  return null
}
```
  * switch
```javascript
switch(isPrimeNum()) {
  case true:
    alert("yes");
  case false:
    alert("no");
}
```

## Javascript 반복문

  * while(조건식) {}
  * for(초기화 문장; 조건식; 증감문) {}
  * do {} while (조건식)

## Javascript 내장 함수

- 크게 함수와 메소드로 구분.
  * eval(): 문자열 입력을 계싼하여 결과를 반환
  * parseInt(), parseFloat(): 문자열을 정수, 실수로 각각 변환
  * setTimeout(function_name, delay_time): 지연시간 후에 매개변수로 지정된 함수 호출

## 사용자 정의 함수

- 형태
```javascript
function fn_name(a, b, c) {
  return a + b + c
}
```
- 매개변수와 인수의 자료형이 같은지 검사하지 않음. 

**매개변수와 인수**: 매개변수(parameter)는 함수를 호출할 때 인수로 전달된 값을 함수 내부에서 사용할 수 있게 해주는 변수. 한편, 인수(argument)는 함수가 호출될 때 함수로 값을 전달해주는 변수.
{: .notice--info}

- 매개변수와 인수의 개수가 같은지 확인하지 않음. 인수가 지정되지 않은 매개변수는 undefined 처리.
- 리턴 값이 있는 경우 return 문으로 값 반환.