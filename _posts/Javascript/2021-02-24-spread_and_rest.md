---
title: "Spread and Rest"
excerpt: "What are Spread and Rest in Javascript"
excerpt_separator: "<!--more-->"
categories:
  - Javascript
tags:
  - Spread
  - Rest
last_modified_at: 2021-02-24T14:20:00
---
<!--more-->

<br>

## Spread - 전개 연산자

  * 배열 내부의 요소들을 빼내기 위해 사용하는 연산자이다.
  * 형태는 '...배열이름'이다.
  
### 함수 및 배열에서의 사용  
  
  * 예를 들어 Math.max() 메소드의 경우 인자로 숫자만 받을 수 있다. 이럴 때, arr[1, 2, 3]과 같은 배열을 인자로 넣기 위해서는 '...arr'을 인자로 넣는 것이 가능하다.
  * 전개 연산자를 여러 개 사용하여 인자로 전달하는 것도 가능하다.
  * 전개 연산자를 통해 새로운 배열을 재조합하는 것도 가능하다.
  
### 객체에서의 사용

  * 아래와 같이 사용하면 새로운 객체를 만들 때 기존 객체의 속성들을 그대로 가져오면서 새로운 속성을 할당할 수 있다.
  
```javascript
    const fruit = {
        name: '과일'
    };
    
    const apple = {
        ...fruit,
        color: 'red'
    };
```
  
### 나머지 매개변수

  * 나머지 매개변수에 대한 연산자로, 형태 자체는 Spread 연산자와 동일하다.
  * Spread 연산자와의 차이점은 Rest는 함수를 정의할 때 표기된다는 것이다. 본 함수가 정해지지 않은 임의의 인자 개수를 받을 수 있을 때, 이를 정리하기 위한 문법으로서 이용된다.
  * 아래의 예1과 같이 사용하면 sumNum 메소드는 인자의 개수에 따라 전체 값의 합을 구해낸다.
  
```javascript
function sumNum(...Nums) {
    let sum = 0;

    for (let num of Nums) sum += num;

    return sum;
}
``` 

  * 아래 예2와 같이 사용하면 지정한 인자 이외에 들어온 인자들을 하나로 묶어 배열로 사용하게 된다. 이 경우 나머지 매개변수는 항상 인수의 마지막에 명시되어 있어야 한다.
  
```javascript
function printProfile(name, age, ...etc) {
    alert(name);
    alert(age);
    alert(etc[0]);
    alert(etc.length);
}
```

## Rest

  * 아래 예시는 어떤 객체가 존재할 때, 새로운 객체를 생성하여 앞서 존재하던 객체의 값을 넣으려는 상황을 묘사하였다. 'name' 속성을 제외한 다른 속성들이 모두 '...rest'에 객체로서 들어가게 된다.
  
```javascript
const phone = {
    name: 'FFFire',
    color: 'Red',
    size: '480 x 300'
}

const { name, ...rest } = phone;
console.log(name);      // FFFire
console.log(rest);      // Object {color: 'red', size: '480 x 300'}
``` 