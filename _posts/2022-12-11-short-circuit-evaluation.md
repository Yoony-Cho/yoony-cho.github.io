---
date: 2022-12-11T00:30:05.000Z
layout: post
published: true
title: "[JavaScript] Type conversion & short circuit evaluation"
subtitle: Type conversion & short circuit evaluation?
description: Let's find out the Type conversion & short circuit evaluation
image: https://pbs.twimg.com/media/EeUg1QtUEAERz5l.png:large
optimized_image: https://pbs.twimg.com/media/EeUg1QtUEAERz5l.png:large
category: JAVASCRIPT
tags:
  - JS
  - CS
  - Code
author: yoony
---

## What is Type conversion?

> 자바스크립트의 모든 값은 타입이 있고, 값의 타입은 의도적으로 변환 할 수 있는 **명시적 타입 변환**과 개발자의 의도와 상관없이 표현식을 평가하는 도중 자바스크립트 엔지에 의해 암묵적으로 타입이 자동 변환되는 **암묵적 타입 변환**으로 구분한다.



## 암묵적 타입 변환

JS 엔진은 표현식을 평가할 대 개발자의 의도와는 상관없이 코드의 문맥을 고려해 암묵적으로 타입을 강제 변환할 때가 있다.

### 1. 문자열 타입으로 변환

피연산자 중 하나 이상이 문자열이므로 문자열 연결 연산자로 연결되어 동작한다.

```javascript
1 + "2" // "12"

//리터럴 템플릿 사용 시

`1 + 1 = ${1 + 1}` // "1 + 1 = 2"  
```

### 2. 숫자 타입으로 변환

산술 연산자의 경우 숫자 값을 만드는 역할을 한다. 즉, 모든 피연사자는 코드 문맥상 숫자 타입이어야 한다.

``` javascript
1 - '1' // 0
1 * '10' // 10
1 / 'one' // NaN
```

### 3. 불리언 타입으로 변환

제어문 또는 삼항 조건 연산자의 조건식은 불리언 값, 즉 논리적 참/거짓으로 평가 되어야 하는 표현식이다. 자바스크립트 엔진은 조건식의 평과 결과를 불리언 타입으로 암묵적 타입 변환 한다.

```javascript
if ('') console.log('1');
if (true console.log('2');
if (0) console.log('3');
if ('str') console.log('4');
if (null) console.log('5');

// 2 4
```



## 명시적 타입 변환

개발자의 의도에 따라 표준 빌트인 생성자 함수를 new연산자 없이 호출하거나 메서드를 사용하는 등 타입 변환을 할 수 있다.

> 반복문을 대체할 수 있는 기능으로는 forEach 메소드, for ...in 문, for ...of문 등이 있다.

### 1. 문자열 타입으로 변환

문자열 타입이 아닌 값을 문자열 타입으로 변환하는 방법

1. String 생성자 함수를 new연산자 없이 호출하는 방법
2. Object.prototype.toString 메서드를 사용하는 방법
3. 문자열 연결 연산자를 이용하는 방법

``` javascript
1. String(1) // "1"
2. (1).toString(); // "1"
3. 1 + '1' // "11"
```

### 2. 숫자 타입으로 변환

숫자 타입이 아닌 값을 숫자 타입으로 변환하는 방법

1. Number 생성자 함수를 new연산자 없이 호출하는 방법
2. parseInt, parseFloat 함수를 사용하는 방법(문자열만 숫자열로 변환 가능)
3. +단항 산술 연산자를 이용하는 방법
4. *산술 연산자를 이용하는 방법

```javascript
1. Number(1) // 1
2. parseInt('-1'); // -1
3. +'0'; // 0
4. '0' * 1 // 0
```

### 3. 불리언 타입으로 변환

불리언 타입이 아닌 값을 불리언 타입으로 변환하는 방법

1. Boolean 생성자 함수를 new연산자 없이 호출하는 방법
2. ! 부정 논리 연산자를 두 번 사용하는 방법

```javascript
1. Boolean('x') // true
2. !!0 // false
```



## 단축 평가

### 1. 논리 연산자를 사용한 단축 평가

논리 연산자 표현식의 평가 결과는 불리언 값이 아닐 수도 있다.
논리합 또는 논리곱 연산자 표현식은 언제나 피연산자중 어느 한쪽으로 평가된다.

```javascript
'Cat' && 'Dog' // "Dog"
//논리곱 연산자는 두 개의 피연산자가 모두 True이면 true를 반환한다.

'Cat' || 'Dog' // "Cat"
//논리합 연산자는 두 개의 피연산자 중 하나만 True이면 true를 반환한다.
```

이처럼 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환하는데 이를 단축 평가라고 한다.

**단축 평가**는 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략하는 것을 말한다.

### 2. 옵셔널 체이닝 연산자

좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고 그렇지 않으면 우항의 프로퍼티 참조를 이어간다.

```javascript
var el = null;

var value = el?.value;
console.log(value); //undefined
```

옵셔널 체이닝 연산자는 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때 유용한다.

하지만 옵셔널 체이닝 연산자는 좌항 피연산자가 false로 평가되는 값이라도 null 또는 undefined가 아닌 0, ' ',  false, NaN 등의 값을 참조하는 경우도 있다.

### 3. null 병합 연산자

null 병합 연산자는 좌항의 피연산자가 null 또는 undefined인 경우에 만 우항의 피연산자를 반환하고 그렇지 않으면 좌하으이 피연산자를 반환한다.

``` javascript
var x = null ?? "default string"
console.log(x); // "default string"

//null이나 undefined가 아닌 false값을 논리합으로 연산한 경우
var x = '' || "default string"
console.log(x); // "default string"

//null이나 undefined가 아닌 false값을 null 병합 연산자로 연산한 경우
var x = '' ?? "default string"
console.log(x); // ""
```
