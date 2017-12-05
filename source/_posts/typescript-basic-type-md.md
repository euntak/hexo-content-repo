---
title: Basic Types
date: 2017-12-01 15:44:39
thumbnail: /images/typescript.svg
tags:
- Typescript
categories:
- Typescript
---
# Typescript Basic Types

Typescript-Intro에서 Typescript는 Javascript의 superset이라고 소개했다.
**그래서 Javascript의 기본 자료형들을 모두 포함한다.**

사용자가 만든 커스텀한 타입들은 결국에 이러한 기본 자료형으로 쪼개지기 때문에 Typescript의 정적 타이핑의 이점을 제대로 활용하기 위해서 반드시 알고 넘어가야한다고 생각되어 살짝 정리해보았다.

우선 Javascript의 기본 자료형을 살펴보자.

* Boolean
* Number
* String
* Null
* Undefined
* Symbol (ES6)
* Array (Object)

Typescript는 위와 동일한 타입을 가지고있으며, 아래와 같이 추가타입을 지원한다.

* Any
* Void
* Never
* Enum
* Tuple (Object)

## Primitive Type

Object를 제외한 모든 유형은 변경이 불가능한 값을 정의한다.
레퍼런스 형태가 아닌 실제 값을 저장하는 자료형이다.

자세한 내용은 [Javascript Primitive Values](https://developer.mozilla.org/ko/docs/Web/JavaScript/Data_structures)를 참고하길 바란다.

## Literal

JavaScript에서 값을 나타내기 위해 리터럴을 사용한다. 이는 말 그대로 스크립트에 부여한 고정값으로, 변수가 아니다. 상수는 가리키는 포인터가 고정이라는 점, 리터럴은 그 자체가 값이자 그릇이다.

```js
['a', 'b']; // array literal
'troflev' // string literal
true // boolean literal
{ obj : 'obj' } // object literal
10 // number literal
```

이러한 값들을 리터럴이라고 하는 이유는 프로그램 내에 직접 문자형태로 지정되는 값들이기 때문이다.
이러한 값들은 한번 지정되면 변하지 않고, 그 값을 변경 할 수 없기 때문이다.

```js
const first = 1;
```

예를 들어, 다음과 같이 first 변수에 할당된 `1`은 그 자체가 값이면서 프로그램내에서 값을 변경 할 수 없기 때문에 이러한 값들을 **리터럴 상수**라고 부른다.

마찬가지로 자세한 내용은 [Javascript Literal](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Values,_variables,_and_literals#Array_literals)을 참고하길 바란다.

## Wrapper Object VS Primitive type

Boolean은 boolean을 래핑한 객체이고, 해당 primitive값을 편리하게 사용하기 위해 `toString(), valueOf()`와 같은 내장 함수들을 제공한다.
boolean은 primitive type이며, Boolean 객체에 할당 할 수 없다.

위 두 타입 중 `boolean`의 사용을 권장하는 편이다. 래핑된 객체 Boolean으로 생성한 값을 boolean으로 할당할 수는 있으나, boolean으로 생성한 값을 Boolean으로 할당 할 수 없기 때문이다.

```js
const boolean1 : boolean = new Boolen(true); // Allow
const boolean2 : Boolean = true; // Error: Type 'Boolean' is not assignable to type 'boolean'.
// 'boolean' is a primitive, but 'Boolean' is a wrapper object. Prefer using 'boolean' when possible.
```

위의 예제를 보면, **boolean1**은 `boolean` 타입을 지정하여 Wrapper Object인 `new Boolean(true)`을 받을 수 있지만, **boolean2**에서 볼 수 있듯이 받는 타입을 Boolean으로 지정하면 `true`값을 받지 못한다. 때문에 가능하면 boolean을 사용하라고 권장한다. (Javascript, Typescript)

`Number / number , String / string`에서도 동일하게 적용된다.

참고로 [Airbnb Javascript Style Guide](https://github.com/airbnb/javascript)를 보면, Javascript에서 Wrapper Object로 값을 생성하는 것 보다 리터럴로 값을 생성하는 것을 권장한다.

이제 본격적으로 Typescript에서 제공하는 기본 타입에 대한 것들을 알아보자.

## Any

이름으로 유추할 수 있듯이 `어떤 타입이어도 상관 없다`라는 뜻이다.
Typescript Compile option에서 `noImplicitAny` 옵션을 사용하여 any를 쓰면 오류를 발생시키도록 하는 옵션을 지정 할 수 있다.

```ts
interface UserInfo {
    name: string;
    age: number;
    address: string;
}

// Type '{ name: string; address: string; }' is not assignable to type 'UserInfo'.
// Property 'age' is missing in type '{ name: string; address: string; }'.
const User1: UserInfo = {
    name: 'name',
    address: 'address'
}

// Allow
const User2: any = {
    name: 'name',
    address: 'address'
};
```

위의 예제를 살펴보면, User1은 타입이 `UserInfo`이고, User2는 `any`타입을 가진 객체이다.
**User1**에서는 타입 체크가 통과되지 못하여 컴파일 단계에서 주석과 같은 에러를 발생시키고, **User2**에서는 타입이 any로 되어 있으므로, `User2에는 아무 값이나 넣어도 문제 없어`라는 말과 같기 때문에 아무런 에러를 발생시키지 않는다.

~~그렇기 때문에 Typescript를 제대로 활용하기 위해서는 `any`를 최대한 사용하지 않는 것!~~
Typescript가 계속적으로 발전하고, IDE나 텍스트 편집기 툴들이 많이 발전하면서 자동으로 Type을 유추해주는 기능들이 발전하고 있다. 때문에 any를 사용해도 그렇게 크게 문제가 될만한 이슈들이 발생하지 않을 수 있게되었지만 **그래도 최대한 안쓰는 걸로.** (Type을 명시해 주면 코드를 읽는 사람들이 빠르게 타입을 유추할 수 있는 이점도 있기도 하고.. 기타 등등..)

## Void

C, Java를 사용해봤다면 익숙한 keyword이다. Typescript에서도 동일한 쓰임새를 보인다. 보통 함수의 리턴 형식을 지정할 때 사용한다.

```ts
function printErrorLog(error: ErrorType): void {
    console.error('Error : ', error);
    return null;
}
```

위와 같이 error log를 출력하고 리턴 값이 없는 함수의 경우 `void` 타입을 명시적으로 지정해 줄 수 있다.
`void`는 `null`, `undefined` 값을 가질 수 있기 때문에, 함수 리턴에 null과 undefined를 지정 할 수 있다.

## Never

얘는 왜 있는 타입인지 모르겠다. 사실 써본적이 없다. `void`와 비슷한 특정을 가지고 있지만, 얘는 null과 undefined를 모두 허용하지 않는다. `any`와 반대되는 타입이다. 모든 것을 허용하지 않는 타입.

```ts
// Function returning never must have unreachable end point
function error(message: string): never {
    throw new Error(message);
}

// Inferred return type is never
function fail() {
    return error("Something failed");
}

// Function returning never must have unreachable end point
function infiniteLoop(): never {
    while (true) {
    }
}
```

## Enum

이 Keyword도 익숙한 부분이 있다. `Enumertaion`을 생각하면 될 듯 하다.

```ts
enum Coffee {
    Espresso,
    Americano,
    Latte
}
const favoriteCoffe = Coffee.Americano; // 'Americano'
```

Enum type은 [Typescript Playground](https://www.typescriptlang.org/play/index.html)에서 실행 해보면 약간 복잡한 Javascript code로 변환되는데 잠깐 살펴보자.

```js
var Coffee;
(function (Coffee) {
    Coffee[Coffee["Espresso"] = 0] = "Espresso";
    Coffee[Coffee["Americano"] = 1] = "Americano";
    Coffee[Coffee["Latte"] = 2] = "Latte";
})(Coffee || (Coffee = {}));
var favoriteCoffe = Coffee.Americano; // 'Americano'
```

`Enum type`은 위와 같은 IIFE(Immediately-invoked function expression) 형식으로 변환이 된다.

위의 코드를 크롬 브라우저 콘솔에서 실행시킨 결과 값이다.

![enum-test](/images/typescript-enum.png)
[이와 같은 결과를 나타내는 이유](https://stackoverflow.com/questions/20278095/enums-in-typescript-what-is-the-javascript-code-doing)

## Tuple

Tuple은 DB에서 주로 들어본 keyword인데, 그 의미가 완전 다르다.
Typescript에서의 Tuple은 배열의 종류로서 타입이 한가지가 아닌 여러 타입을 허용하는 특이한 배열이다. 배열이므로 수정과 삭제 추가가 가능한 특징을 갖는다.

```ts
let tuplex: [ boolean, number ] = [false, 100];
tuplex.concat([ true, 200 ]);
tuple.push('string'); // Argument of type '"string"' is not assignable to parameter of type 'number | boolean'.
tuplex.push([100, true]); // Argument of type '(number | boolean)[]' is not assignable to parameter of type 'number | boolean'. Type '(number | boolean)[]' is not assignable to type 'false'.
tuplex.push([100]); // Argument of type 'number[]' is not assignable to parameter of type 'number | boolean'. Type 'number[]' is not assignable to type 'false'.
```

위와 같은 예제를 보면, 배열의 타입을 지정 할 수 있다. 각 타입이 지정된 배열의 `순서대로` arguments들이 들어와야 하며, 지정된 타입 외에 `다른 타입의 값을 할당할 수 없다`. 또한 처음 `선언된 타입의 개수만큼` arguments들이 지정 되어야 한다.

---

오늘은, Typescript의 기본 타입들을 살펴보았다. 개인적으로 Typescript를 공부하면서 적은 글이라 설명이 많이 부족한 것 같다. 이 글을 읽으면서 부족한 점이 있거나 틀린점이 있다면 언제든지 지적해주길 바란다.
