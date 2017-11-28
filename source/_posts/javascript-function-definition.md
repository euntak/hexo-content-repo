---
title: Javascript Function
date: 2017-10-20
thumbnail: /images/javascript.svg
tags:
- Javascript
categories:
- Javascript
---
# Javascript Function Definition

자바스크립트에서의 함수를 정의하는 방법에 대해서 알아보도록 하겠습니다.

* Function Declaration
* Function Expression
* new Function(param1, param2, body) 객체로 생성하기

### Function Declaration (함수 선언문)

```js
function book() {
    return 'JS';
}
```

### Function Expression (함수 표현식)

```js
var outside = function inside(param) {
    if(param === 102) return param;
    return inside(param + 1);
}
console.log(outside(100));
```

자바스크립트 엔진이 해석하는 KEY VALUE 변경 해보면 { outside : { indide : Funtion Object } }

### 함수 선언문과 표현식의 차이

가장 큰 차이점은 `Hoisting`에 있습니다.

```js
deff(); // called deff
function deff() {
    console.log('called deff');
}

geff(); // error!
var geff = function() {
    console.log('called geff');
}
geff(); // called geff
```

위와 같은 예제에서, `deff`와 `geff` 두 함수를 호출할 때에, 함수 표현식으로 선언이 된 geff는 익명의함수가 할당된 다음에 geff()를 호출하게 되면, 정상적으로 작동이 되게 됩니다.

함수 선언문은 Function Object가 Key, Value로 등록되는 특징상 같은 실행 컨텍스트에서 함수의 이름을 중복해서 작성 할 수 없기 때문에 함수 표현식으로 `Namespace`를 이용해서 이와 같은 문제를 해결 할 수 있습니다.

> 함수 선언문은 Hoisting이 되기 때문에, Global Scope로 Function Object가 등록이 되어 어디서든지 사용할 수 있게 되고, 함수 표현식은 Hoisting이 되지 않기 때문에, 해당 변수에 함수를 할당하는 과정 이후에만 사용 할 수 있다.

### 함수 선언문 오버라이딩

함수 이름이 같을 때 함수 코드 대체 (replace)

* JS는 파라미터 수, 데이터 타입을 체크하지 않는다
  * Why? Function Object는 {key : value} 형식으로 저장되기 때문
  * 고로 Function Signiture는 **Only 함수 이름** 
* 초기화 단계에서 함수 선언문을 `Funtion Object`로 생성
* 코드 진행 중, 아래에 이름이 같은 함수 선언문이 있으면 `Overriding (replace)`된다.

```js
function first() {
    console.log('first');
}

function first(i) {
    console.log('second');
}

console.log(first()); // second
```

### Do it

다음과 같이 코드를 작성 했을 때에 예상 결과를 한번 생각해보기.

1. 함수 선언문 - `first()` - 함수 선언문
2. 함수 표현식 - `second()` - 함수 표현식
3. 함수 선언문 - `third()` - 함수 표현식
4. 함수 표현식 - `fourth()` - 함수 선언문

`debugger;`를 통해서 실행 Context 및 순서 확인하기

```js
window.onload(function () {
    debugger;
    function first() { console.log('first'); };
    console.log(first());
    function first() { console.log('first2'); };

    var second = function () { console.log('second'); };
    console.log(second());
    var second = function () { console.log('second2'); };

    function third() { console.log('third'); };
    console.log(third());
    var third = function() { console.log('third2'); };

    var fourth = function () { console.log('fourth'); };
    console.log(fourth());
    function fourth () { console.log('fourth2'); };
});
```

> 1, 4번의 경우에는 `Function Overriding`이 일어 난다. 때문에, 함수 표현식에서의 `fourth`의 값이 JS 엔진에 의해서 초기화 될 때에 `undefined`가 아닌 이전의 함수 선언문에서 정의 했던 `FO`가 초기 값이 된다.