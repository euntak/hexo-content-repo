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

딱히 정해져 있지 않는 것 같다. 보통 새로운 사용자 정의 타입을 사용하거나, Union Type과 같이 여러개의 타입을 지정하거나, Intersection Type을 지정 할 때 많이 사용하는 것 같다.

### 불편

```ts
function testFunc(arg: string | number): string | number {
    return arg;
}
```

### 편안

```ts
type StringOrNumber = string | number;
function testFunc(arg: StringOrNumber): StringOrNumber {
    return arg;
}
```

## Type Alias VS Interface

Interface와 비슷한 역할을 하지만, 사실 Interface와 가장 큰 차이점이 두가지 있는데 한번 살펴보도록 하자.