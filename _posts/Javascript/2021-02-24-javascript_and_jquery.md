---
title: "The Meaning of '$' in Javascript"
excerpt: "Meaning of '$' in Javascript / Javascript and Jquery"
excerpt_separator: "<!--more-->"
categories:
  - JavaScript
tags:
  - $
  - Jquery
last_modified_at: 2021-02-24T10:30:00
---
<!--more-->

<br>

## Javascript에서 '$'란 무엇인가?

  * Javascript에서 흔히 볼 수 있는 '$'라는 표현은 Jquery 관련 표현을 사용하겠다는 의미이다.
  * 이는 html의 태그나 css를 지정하고 이벤트를 조작하는데 더욱 간결한 코드와 편리함을 가져다 준다.
  
## Jquery란?

  * Jquery란 Javacript의 라이브러리 중 하나이다.
  * 클라이언트에서 html을 조작하는데 더욱 편리함을 주기 위해 고안된 것으로, HTML 문서 탐색 및 조작, 이벤트 처리, 애니메이션 및 Ajax와 같은 작업을 훨씬 간단하게 한다.

## Jquery를 사용하는 이유

  * 같은 코드를 작성함에 있어 순수 Javascript를 사용하는 경우와 Jquery를 사용하여 표현한 경우는 코드의 길이면에서 큰 차이를 보인다. 이는 Jquery로 작성된 코드의 가독성을 더 높이는 효과도 가지고 있으며, 개발자들로 하여금 개발 효율을 높이는 결과를 가져올 수 있다.
  * 아래의 예시는 같은 내용의 순수 Javascript 코드와 Jquery 코드를 제시한 것이다.
  
```javascript
[Javascript]

<script>
function changeText() {
    var target = document.querySelectorAll('.tagId');
    target.forEach(function (element) { 
        element.text('La-la-la')
    });
}
```

```javascript
[Jquery]

$('.tagId').text('La-la-la')
```

## JS와 JQ, 어떻게 써야하는가?

  * 위의 내용만 보면 Jquery의 사용이 무조건적으로 권장되는 것으로 보여진다. 그러나 Jquery는 코드 작성 효율에는 큰 이점이 있는 반면, 코드 처리 속도 면에서는 오히려 느리다는 단점이 있다.
  * Jquery는 Javascript의 라이브러리로서 몇 줄, 혹은 몇 개의 구성으로 이루어진 코드 기능을 간단하게 표현할 수 있도록 하였는데, 이는 다시 말해 몇 가지의 코드 처리에 수많은 과정들이 내포되었음을 의미한다. 그러므로 무분별한 Jquery의 사용은 불필요한 과정을 포함시켜 역으로 나쁜 효율을 보여주기도 한다.
  * 따라서 Javascript와 Jquery를 혼용하여 적절하게 사용하는 것이 필요하다. 특히 연산량이 많아지는 반복문에서는 Javascript로 처리 속도면에서 효율을 끌어낼 수 있도록 방법을 고안하자. 