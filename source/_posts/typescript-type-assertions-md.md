---
title: Type Assertion
date: 2017-12-04 21:57:01
thumbnail: /images/typescript.svg
tags:
- Typescript
categories:
- Typescript
---
# Type Assertion

Type Assertion은 쉽게 말해 Typescript Compiler에게 `이녀석의 타입은 이것이야`라고 알려주는 것을 의미한다.

> **개발자 - 내가 이녀석의 타입을 더 잘 아니까 넌 내가 정한 타입에 토달지 말고 컴파일이나 열심히해**
> **컴파일러 - OK! 대신에 런타임 에러나면 니 책임**
극단적인 대화지만... 그만큼 개발자(작성자)가 100% 타입을 확신한다는 가정하에 사용이 되어야 한다.

## 문법

Type Assertion의 문법은 다음과 같이 두가지이다.

1.**변수 `as` 강제할 타입**
2.**`<강제할 타입>` 변수**

```ts
const x = <any> foo;
// is equivalent to:
const x = foo as any;
```

## `as Foo` vs `<Foo>`

`<Foo>`가 원조 `as Foo`가 뉴페이스인데, `as operator`는 사실 JSX 표현식을 지원하기 위해서 나왔다.

```ts
//tsx
const foo: any;
const bar = <string> foo; // bar is now of type "string"
```

```ts
//jsx
const foo = <string>bar;
</string>
```

Typescript 1.6에서 `.tsx` 파일 확장자와 `as operator`가 처음 소개 되었는데 기존의 Typescript에서 사용했던 **`<any>와 같은 접두어 방식`과 `JSX 표현식` 사이의 모호함을 없애고 일관성을 위해서 최근에 새로 만든 `as operator`의 사용을 권장한다.** ~~라고 나와있는데 사실 JSX를 쓰는 것이 아니라면 둘 중 아무거나 사용해도 상관 없을 듯 하다. 하지만 난 쓰라는거 써야지~~

## 간단한 예제

보통은 Union과 같은 여러가지의 타입을 가질 수 있는 데이터에서 타입을 강제로 지정하거나, superset이 되는 타입을 지정하는 경우(그 반대의 경우도), 혹은 Javascript 코드를 Typescript코드로 이식할 때 많이 쓰인다고 한다.

```ts
const foo = {};
foo.bar = 123; // Error: property 'bar' does not exist on `{}`
foo.bas = 'hello'; // Error: property 'bas' does not exist on `{}`
```

위와 같은 Typescript 예제에서는 foo 객체에 `bar, bas`프로퍼티가 없으므로, 해당 프로퍼티에 값을 할당 할 수 없다는 에러가 발생하게 되는데 이를 Type Assertion을 적용하면 다음과 같이 간단하게 해결할 수 있다.

```ts
interface Foo {
    bar: number;
    bas: string;
}
const foo = {} as Foo;
foo.bar = 123;
foo.bas = 'hello';
```

## Type Casting VS Type Assertion

처음 Type Assertion을 접했을 때 형변환과 비슷한 느낌으로만 이해 하고 있었는데, 형변환의 개념이랑은 약간 차이가 있다.

형변환(Type casting)은 **런타임 환경을 지원하고 데이터의 실제 구조를 변경한다.**
Type Assertion은 **컴파일 타임 구조**이며 **컴파일러가 코드를 분석하는 방법에 대한 힌트를 제공한다는 점**에서 차이점이 있다.

## 사용은 신중히

Assertion을 사용하게 되면 레거시 코드 마이그레이션이 쉽게 허용이 되기 때문에 항상 신중하게 사용하자.

```ts
interface Foo {
    bar: number;
    bas: string;
}
const foo = <Foo> {};
// ahhhh .... forget something?
```

예들 들어, 위와 같은 코드에서 foo에 대해 `autocomplete`를 제공하지만, 개발자(작성자)가 properties를 모두 작성하는 것을 까먹을 수도 있고, 나중에 리펙토링 할 때 쉽게 깨질 수 있다는 단점이 있다. (예: 새로운 property의 추가/삭제/수정 등..) 이런 단점들은 에러를 발생시킬 수 있는 요인이 될 수 있다.

Typescript를 사용하면서 얼마나 자주 쓰일지는 모르겠지만, 잘 이해하고 사용하는 것이 좋을 것 같다. ~~뭐든지 잘 쓰면 좋지만 그게 어렵다는 점~~

---

### 마치며

[Typescript Handbook](https://basarat.gitbooks.io/typescript/docs/types/type-assertion.html)을 참고하여 작성하였습니다. 
설명이 부족하거나 틀린 부분이 있으면 댓글로 지적해주시면 감사하겠습니다.