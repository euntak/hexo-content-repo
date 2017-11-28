---
title: Javascript Hoisting
date: 2017-10-20
thumbnail: /images/javascript.svg
tags:
- Javascript
categories:
- Javascript
---
# Javascript Hoisting

Javscript Hoisting을 이해하기 위해서는 먼저 Javascript에서의 함수 정의 방법에 대한 이해가 필요합니다.

```js
function sports() {
    debugger;
    var player = 11;
    function soccer() {
        return player;
    }
    var baseball = function() {};
    soccer();
};
sports();
```

- 위와 같은 코드에서 Javscript Engine은 어떻게 동작할까?
  - 모든 Javascript Function은 다음과 같이 동작한다.
  - 첫번째 cycle 돌면서 `함수 선언문`을 찾아 FO(function object)을 등록
  - 두번째 cycle 돌면서 `변수 (var)`를 찾아 `undefined`로 초기화
  - 세번째 cycle 돌면서 JS 코드 해석 및 `debugger;` 동작
  - 함수 선언문 해석
    - function sports(){};
  - 변수 초기화
    - var player; // undefined
    - var baseball; // undefined
  - JS 코드 실행
    - debugger;
    - var player = 11;
    - var baseball = function() {};

> 이러한 과정을 “호이스팅(Hoisting)”이라고 칭하며, “var”로 등록된 변수나, “function” 키워드로 등록된 “함수 선언문”이 JS 엔진에 의해서 해석될 때에 “위로 당겨진다(Hoisting)”라는 이유도 이러한 JS 엔진이 코드를 분석하는 특징 때문에 생겨난 개념인 것이다.