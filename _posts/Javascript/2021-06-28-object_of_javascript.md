---
title: "Object of Javascript"
excerpt: "Objects of Javascript and How To Use Them"
excerpt_separator: "<!--more-->"
categories:
  - JavaScript
tags:
  - Object
last_modified_at: 2021-06-28T17:51:00
---

<!--more-->

<br>

## Javascript 객체

- 자바스크립트 객체는 내장 객체와 사용자 정의 객체로 구분
- 자바스크립트 객체는 속성과 메소드를 가짐
- 객체 속성 값으로 또 다른 객체를 가질 수 있는 계층적 구조

## 내장 객체

- 자바스크립트가 제공하는 Array, Date, Math, String
- 웹 브라우저가 제공하는 window, navigator, document

## Javascript가 제공하는 내장 객체

#### Date 객체: 컴퓨터에서 제공되는 날짜와 시간을 담은 객체
  * 메소드
    * getFullYear(): 연도
    * getMonth(): 월
    * getDate(): 일
    * getDay(): 요일
    * getHours(): 시간
    * getMinutes(): 분
    * getSeconds(): 초
    * getTime(): 1970년 1월 1일 이후 현재까지의 시간을 ms 단위로 리턴
    * getTimezoneOffset(): 표준시와 현지 시간의 차이를 분 단위로 표현
    * setFullYear(): 연도 설정
    * setMonth(): 월 설정
    * setDate(): 일 설정
    * setDay(): 요일 설정
    * setHours(): 시간 설정
    * setMinutes(): 분 설정
    * setSeconds(): 초 설정
    * setMillseconds(): millisecond 값 설정

#### Math 객체: 널리 알려진 상수나 함수들에 대한 객체. 별도의 선언이나 생성과정 없이 바로 사용 가능.
  * 속성
    * E: 자연 상수
    * LN2: 자연로그 2
    * LOG2E: loge / log2
    * PI: 파이(3.14...)
    * SQRT2: 루트 2
  * 메소드
    * cos(), sin(), tan(): 삼각함수
    * acos(), asin(), atan(): 삼각함수의 역함수
    * ceil(), floor(), round(): 올림, 내림, 반올림
    * max(), min(), abvs(): 최대, 최소, 절대값
    * sqrt(x), pow(x, y): 루트 x, x의 y승
    * log(x), exp(x): x의 자연로그, e의 x승

#### 배열 객체:
  * 배열의 각 요소는 동일한 자료형이 아니어도 됨.
  * 배열의 크기는 유동적
  * 배열의 생성은 new 연산자를 이용하거나 배열 리터럴을 이용한다.
    * ex) var book_arr = new Array("a", "b", "c");
    * ex2) var book_arr2 = ["a", "b", "c"];
    * ex3) var arr100 = new Array(100);
  * 배열 요소는 배열이름[인덱스]와 같이 접근한다.
  * 배열 사용법
    * arr[4] = "1 + 2"; <= 원소 추가
    * arr.length = 3; <= 배열 축소(초과되는 원소 제거)
    * arr[1000] = 1000; <= 중간 인덱스 값들은 없는 상태로 추가 가능
  * 배열 객체 메소드
    * reverse(): 요소들의 순서를 반대로
    * sort(): 요소들의 순서를 오름차순으로. 숫자도 문자열로 변환하여 순서 결정 후 다시 숫자로 되돌린다.
    * join(): 배열 내 요소를 모두 연결한 하나의 문자열을 생성. 요소 사이에 끼워 넣을 문자열을 지정할 수 있음.
    * concat(): 배열 뒤에 요소를 붙여서 배열 내용을 추가
    * slice(): 배열의 요소들 중 일부만을 새로운 배열로 만듦.

## 브라우저 제공 내장 객체

#### window 객체
  * 브라우저 창에 대한 객체
  * open(): 새로운 창을 여는 메소드
  * close(): 열려 있는 창을 닫는 메소드
  * alert(), confirm(), prompt()

#### navigator 객체
  * 브라우저 정보를 갖고 있는 객체(브라우저 버전 등)

#### document 객체
  * HTML 문서에 대한 객체

## 사용자 정의 객체
- 생성방법 1: new 명령어로 Object 생성 후 속성 및 메소드를 동적으로 추가 가능
```javascript
var book = new Object();
book.title = "자바스크립트 정리";
```
- 생성방법 2: 초기화를 통한 객체 생성
```javascript
var book = {title: "자바스크립트 정리"};
```
- 접근방법: .을 통해 접근. 속성의 이름을 모르더라도 for 문으로 접근 가능.
```javascript
for (var p in book) {}
```
- 객체에서 속성을 삭제
```javascript
delete book.title;
```

## 객체 생성자
- 생성자 함수: 객체를 생성하는 함수
- this: 객체 자신을 지칭하는 키워드
- 객체의 속성값으로 함수를 저장하면 그 객체의 메소드가 된다.
```javascript
function Book(title_value) {
    this.title = title_value;
}
```
