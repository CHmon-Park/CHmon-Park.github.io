---
title: "Computed vs Methods vs Watch"
excerpt: "What Difference among computed, methods, watch"
excerpt_separator: "<!--more-->"
categories:
  - Vue.js
tags:
  - Vue.js
  - JavaScript
  - VS Code
last_modified_at: 2021-02-13T14:20:00
---
<!--more-->

<br>

## Computed vs Methods

  * 두 기능은 모두 html에서 함수와 비슷하게 사용된다고 할 수 있다.
  * Computed는 html에서 <함수 이름> 의 형태로 사용되고,
  * Methods는 <함수 이름>() 형태로 사용된다.

#### 공통점

  * 두 기능은 Vue.js의 script 영역에서 명시된다.

#### 차이점

  * methods는 component가 관리하는 데이터가 변경되는 순간마다 재실행이 되나, computed는 자신이 사용하는 데이터가 변경될 때에만 재실행이 된다. 즉, 함수 실행의 효율성에서 차이가 있다고 할 수 있다.
  * methods가 인자를 전달받아 처리를 할 수 있는 반면, computed는 인자를 전달할 수 없다.
  * computed의 경우 반드시 return 값이 존재해야 한다. 


## Computed vs Watch

  * 두 기능은 모두 자신에게 종속되어 있는 데이터의 상태에 따라 함수 실행의 여부가 결정된다는 공통점이 있다.
  
#### 공통점

  * 자신에게 종속되어 있는 데이터가 변함에 따라 함수가 실행된다.
  * 두 기능은 Vue.js의 script 영역에서 명시된다.

#### 차이점

  * computed의 경우 html 코드 안에서 출력 명령이 있어야지만 함수가 실행되어 결과값을 출력하지만, watch는 특정 데이터의 변화를 감지하여 자동으로 함수를 실행한다.