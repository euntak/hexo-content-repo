---
title: Typescript Intro
date: 2017-12-01
thumbnail: /images/typescript.svg
tags:
- Typescript
categories:
- Typescript
---
# Typescript Intro

> Typesciprt는 *무료* 그리고 Microsoft(이하 MS)에서 개발 및 유지 관리하는 *open-source programming language*다.

Javascript의 superset이며, 언어에 정적인 타입을 선택적으로 추가할 수 있는 장점이있다.

## History

TypeScript는 대규모 응용 프로그램을 개발할 때 JavaScript의 단점에서 비롯되어서 개발되었다.

Javascript 짜여진 프로그램의 규모가 커지면 커질 수록, 복잡한 구조를 가질 수 밖에 없게 되고, 개발을 하는 입장에서 디버깅하기가 매우 까다로워질 수 밖에 없다.

> ECMA 曰 "향후에는 class-based programming에 대한 지원을 할꺼야. 이건 표준 문서에도 적혀있는 거란다."

MS에서는 ECMA의 표준을 지키며 크로스 플랫폼 지원과 호환성을 손상시키지 않는 솔루션을 찾게 되었고, Javascript의 단점들을 보완할 수 있는 추가 확장 기능들을 사용하기 위해서 Basic Javascript로 변환 하는 Compiler를 개발하게 되었다.

Typescript는 MS에서 내부적으로 2년의 개발기간을 거친 후 2012년에 0.8 버전으로 처음 발표되었다.
하지만 OS X와 Linux에서는 사용 할 수 없었고, 지원되는 IDE도 Microsoft Visual Studio밖에 없었기 때문에 부정적으로 평가를 받기도 했다.

하지만, 2013년에 0.9 버전이 나오면서 플러그인을 통해서 여러 IDE 및 텍스트 편집기들을(Eclipse, Sublime, Vim, Emacs 등등..) 지원할 수 있게되면서 이러한 단점들을 보완하게되었고 추가적으로 Generics도 지원하게 된다.

이 후, 2014년에 진행된 Microsoft Developer Conference에서 Typescript 1.0가 발표되었고, Visual Studio 2013은 Typescript를 built-in하는 업데이트가 되면서 본격적으로 MS의 Typescript 밀어주기가 시작된 것 같다.

2014년 7월에는 Compiler가 이전에 비해 5배의 퍼포먼스를 낼 수 있는 만큼 성능이 대폭 상승함과 동시에 CodePlex에서 관리되던 소스코드를 Github으로 옮겼다.

Typescript는 지속적으로 업데이트 되어 현재 (2017.12.01) 기준 Typescript의 버전은 2.6이다.

## Superset

![superset](/images/venn_typescript_es6_es5.png)

History를 보면 알다시피 Typescript는 Compiled Language이기 떄문에, Typescript로 작성한 코드는 모두 Javascript로 컴파일 된다. 사실 여기서의 컴파일과 전통적인 컴파일 언어(C,C++,C#,Java...)에서의 컴파일은 차이가 있다. 그렇기 때문에 Transpile이라는 용어를 사용하기도 한다.

![transpiling](/images/transpiling.png)

[Typescript Playground](https://www.typescriptlang.org/play/index.html) 에서 확인하면 컴파일(Transpile)된 결과물을 볼 수 있다.

![typescript-playground](/images/typescript-playground.png)

## Why Typescript

일단 Javascript에 익숙한 개발자라면 문법적으로 추가된 기능들에 대한 공부만 조금 하면 큰 허들 없이 써볼 수 있는 장점이 있는 것 같다.

또, 주관적이지만 제품을 만들때에는, 성능도 중요하지만 더 중요한건 안정성인것 같다.
아무리 성능이 좋다고 하더라도 제품이 중간에 뻗는 경우가 발생하면 성능은 무용지물이지 않는가. Typescript는 정적타이핑을 통해 얻는 장점들을 Javascript에 적용할 수 있기 때문에 Javasript에 비해 안정성을 어느정도는 보장해주는 것 같다.

만약 Javascript로 대규모 어플리케이션을 만들 계획을 하고 있다면 Typescript를 추천한다.

## Fuatures

* Type Annotations and compile-time type checking
* Type Interface
* Type erasure
* Interfaces
* Enumerated type
* Mixin
* Generic
* Namespaces
* Tuple
* Await