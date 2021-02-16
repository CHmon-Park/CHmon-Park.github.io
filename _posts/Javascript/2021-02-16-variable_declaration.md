---
title: "Variable Declaration"
excerpt: "Difference among let, var, const"
excerpt_separator: "<!--more-->"
categories:
  - JavaScript
tags:
  - Declaration
  - let
  - var
  - const
  - function-scoped
  - block-scoped
  - hoist
  - TDZ
last_modified_at: 2021-02-16T14:00:00
---
<!--more-->

<br>

## 변수 선언 방식

  * 변수를 사용하기에 앞서서 우리는 그 변수를 선언하여 자료형이나 용법에 제한을 둘 수 있다.
  * Javascript의 경우 ECMA 5 까지는 'var'라는 선언 방식을 가지고 모든 변수를 선언하였는데, 사용의 한계에 부딪혀 ECMA 6 에서 'let', 'const' 라는 대체재가 나오게 된다.
  
## var, let, const의 차이점
  
  * var vs let/const
    * var의 경우 function-scoped이고 let과 const는 block-scoped이다. 즉, var의 경우 함수 내에서 모두 사용이 가능하도록 설정되지만, let과 const는 중괄호 블록 내에서만 유효하도록 설정된다.
  * let vs const
    * let은 선언 후에 값을 할당하는 것이 가능하지만, const의 경우 변수 선언과 동시에 값이 할당되어야 한다.
    * let은 값을 할당한 후 재할당이나 수정이 가능하지만, const의 경우 처음 할당한 값을 변경하는 것이 불가능하다.
    
## Hoist 개념

  * Hoist란 함수 내의 선언들을 해당 함수 유효 범위의 최상단에 선언하는 것을 의미한다.
  * Hoist의 또 다른 설명으로는 메모리에 올라가 있는 변수를 읽는 과정이라고 할 수 있다.
  * Hoist의 대상은 var 선언문이나 function 선언문이 해당한다. 즉, 참조와 선언의 순서로 코딩이 되어 있더라도 선언문이 최상위에서 먼저 다뤄지기에 오류가 발생하지 않게 된다.
  * 다만, 선언문 부분만 Hoist가 되기에 아래와 같은 코드는 나뉘어 해석된다. 따라서 위와 같은 순서로 코딩이 되어 있으면 참조한 값이 아직 들어가지 않아 undefined가 출력된다.
```js
    var menu = 'A course';       // ==> var menu; + menu = 'A course'; 
```
  * 참고로, let과 const도 Hoist가 된다.
  
## TDZ(Temporal Dead Zone)

  * 변수의 생성 단계는 선언, 초기화, 할당으로 나뉜다.
    * 선언(Declaration phase): 변수를 실행 컨텍스트의 변수 객체에 등록하는 단계. 이 단계부터 스코프가 해당 변수 객체를 참조하게 된다.
    * 초기화(Initialization phase): 실행 컨텍스트에 존재하는 변수 객체에 선언 단계의 변수를 위한 메모리를 만드는 단계. 메모리에 올라가는 초기값은 undefined이다. 
    * 할당(Assignment phase): 초기화가 완료된 변수(메모리)에 값을 할당하는 단계.
  * TDZ는 변수의 생성 단계인 선언, 초기화, 할당 중 scope의 시작 지점부터 초기화 시작 지점까지의 구간을 의미한다.
  * var의 경우 선언 단계와 초기화 단계가 한 번에 이루어지기에 선언 이전에 값을 load 하여도 참조가 가능하다. 다만, 그 값은 undefined 상태이다.
  * let의 경우 선언 단계와 초기화 단계가 따로 진행되기에 그 사이에 간극, 즉 TDZ가 존재한다. 특히 초기화 단계에서 메모리에 올라가고 undefined 값으로 초기화가 되는데, TDZ는 그 이전 상태이므로 참조하는 것 자체가 불가능하다.
  * hoist 추가 조사 필요.. let도 hoist가 된단다
