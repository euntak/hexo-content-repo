---
title: Type Alias
date: 2017-12-05 22:30:21
thumbnail: /images/typescript.svg
tags:
- Typescript
categories:
- Typescript
---
# Type Alias

Alias 뜻 그대로 별칭을 붙여주는 역할을 한다.

```sql
SELECT column_name AS alias_name
FROM table_name;
```

위와 같은 데이터베이스 쿼리문에서 `AS`라는 키워드를 볼 수 있는데, 이는 `Alias`의 뜻을 가지며 실제로 그렇게 불린다.
**alias_name이 column_name의 별칭인 것이다.** 이전 포스트(Type Assertion)에서 다루었던 `as`와 혼동하지 말자. ~~마땅히 떠오르는 예제가 이것밖에 없는데 하필~~

Typescript에서도 동일한 의미를 지닌다고 볼 수 있는데, Type에 별칭을 붙여주는 방식이 Type Alias인 것이다.

## 문법

[Typescript Handbook](https://github.com/Microsoft/TypeScript/blob/master/doc/spec.md#3.10)에는 이렇게 정의되어 있다.
`type`&emsp;*BindingIdentifier*&emsp;*TypeParameters<sub>opt</sub>*&emsp;`=`&emsp;*Type*&emsp;`;`

예제를 살펴보자.

```ts
type StringOrNumber = string | number;
type Text = string | { text: string };
type NameLookup = Dictionary<string, Person>;
type ObjectStatics = typeof Object;
type Callback<T> = (data: T) => void;
type Pair<T> = [T, T];
type Coordinates = Pair<number>;
type Tree<T> = T | { left: Tree<T>, right: Tree<T> };
```

## 언제 사용하는 걸까

딱히 정해져 있지 않는 것 같다. 보통 새로운 사용자 정의 타입을 사용하거나, Union Type과 같이 여러개의 타입을 지정하거나, Intersection Type을 지정 할 때 많이 사용하는 것 같다. 말로 설명하는 것 보다 코드를 보면 좀 더 명확하게 이해할 수 있을 것이다.

### 불편

```ts
function testFunc(arg: string | number): string | number {
    return arg;
}
```

**testFunc**함수는 받는 파라미터의 타입이 `string | number`이며, 리턴타입도 동일하다.
저런 형식의 함수가 하나면 저렇게 써도 무방하겠지만, 여러곳에서 저렇게 쓰인다면? interface를 만들어서 빼거나, Type alias로 지정하는 것이 코드를 유지보수하는데 있어서 훨씬 유리할 것이다.

### 편안

```ts
type StringOrNumber = string | number;
function testFunc(arg: StringOrNumber): StringOrNumber {
    return arg;
}
```

## Type Alias VS Interface

type alias는 사용하다보면 interface와 비슷하다는 느낌을 받을 수 있을 것 같다.
사실 Interface와 비슷한 역할을 하지만, Interface와 차이점이 있는데 한번 살펴보도록 하자.

1.Interface는 `multiple merged declarations`를 지원한다.

```ts
interface Person {
  name: string;
  age: number;
}
// ..later
interface Person {
  address: string;
}

const man: Person = {
    name: 'name',
    age: 10,
    address: 'address'
}
```

위의 예제와 같이 **중복된 interface선언**에 대해서 Compiler는 중복 선언한 Interface를 하나로 merge해준다.

2.Interface는 `extends, implements`가 가능하다.

```ts
Interface A {
    //some property
}

Interface B extends A {
    //some property
}

class AB implements A,B {
    // something
}
```

위와 같이 Interface간에 `extends`와, Class에 `implements` 가능하다.

3.Interface는 새로운 타입을 만드는 것이라면, Type Alias는 만들어진 타입의 reference로 사용하는 것이다.

## 정리

일반 객체 유형을 사용하는 경우 인터페이스가 더 나은 방법이다.
인터페이스로 쓸 수 없는 것을 쓰고 싶거나 타입에 뭔가 다른 이름을 주고 싶다면 type alias를 사용하자.