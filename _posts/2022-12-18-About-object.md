---
date: 2022-12-11T00:30:05.000Z
layout: post
published: true
title: "[JavaScript] Object"
subtitle: What is a Object?
description: Let's find out the Object in JavaScript
image: https://pbs.twimg.com/media/EeUg1QtUEAERz5l.png:large
optimized_image: https://pbs.twimg.com/media/EeUg1QtUEAERz5l.png:large
category: JAVASCRIPT
tags:
  - JS
  - CS
  - Code
author: yoony
---

## What is a Object?

> 자바스크립트는 객체 기반의 프로그래밍 언어이며, **자바스크립트를 구성하는 거의 모든 것이 객체다.**



## 객체란?

객체는 0개 이상의 프로퍼티로 구성된 집합이며, 프로퍼티는 키와 값으로 구성된다.

자바스크립트의 함수 또한 일급 객체이므로 값으로 취급할 수 있다.

이때, 일반 함수와 구분하기 위해 프로퍼티 값으로 사용하는 함수는 메서드라고 부른다.

- 프로퍼티 : 객체의 상태를 나타내는 값
- 매서드 : 프로퍼티를 참조하고 조작할 수 있는 동작

```javascript
var circle = {
  radius : 5,                <==== 프로퍼티
  
  getDiameter: function () {
    retrun 2*this.radius;    <==== 메서드
  }
}

console.log(circle.getDiameter()); // 10
```



## 객체 리터럴에 의한 객체 생성

> 자바스크립트는 프로토타입 기반 객체지향 언어로서 클래스 기반 객체지향 언어와는 달리 다양한 객체 생성 방법을 지원한다.

- 클래스 (ES6)
- Object.create 메서드
- 생성자 함수
- Object 생성자 함수
- **객체 리터럴**

이러한 객체 생성 방법 중에서 가장 일반적이고 간단한 방법은 객체 리터럴을 사용하는 방법이다.

객체 리터럴은 줄괄호 ({...}) 내에 0개 이상의 프로퍼티를 정의한다.
변수에 할당하는 시점에 자바스크립트 엔진은 객체 리터럴을 해석해 객체를 생성한다.

``` javascript
var person = {
  name: 'Cho',
  sayHello: function (){
    console.log(`Hello! My name is ${this.name}`)
  }
}
```



## 프로퍼티

프로퍼티에 접근하는 방법은 다음과 같이 두 가지다.

- 대괄호 표기법


- 마침표 표기법

``` javascript
var person = {
  name: 'Cho'
};

//마침표 표기법에 의한 프로퍼티 접근
console.log(person.name);     // Cho
//대괄호 표기법에 의한 프로퍼티 접근
console.log(person['name']);  // Cho
```



### 프로퍼티 값

- 프로퍼티에 값을 할당하면 값이 갱신된다.
- 존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가된다.
- delete 연산자는 객체의 프로퍼티를 삭제한다.



## 원시 값과 객체의 비교

> 자바스크립트가 제공하는 7가지 데이터 타입은 크게 원시 타입과 객체 타입으로 구분할 수 있다.

### 1. 원시 값

원시 타입의 값. 즉 변경 불가능한 값이다.
하지만 변경 불가능하다는 것이 변수 값을 변경할 수 없다는 의미가 아니다.
변수는 언제든 재할당을 통해 변수 값을 변경할 수 있다.

![img](https://velog.velcdn.com/images%2Fmr_chu%2Fpost%2F6eec5b62-8105-483e-bfff-088b9318c8dd%2F%EB%B3%80%EC%88%98%20%EC%9E%AC%ED%95%A0%EB%8B%B9.jpeg)

위 그림처럼 변수는 주소를 가지고 있고 값이 재할당 되면 그 메모리 안에 있는 값이 변하는것이 아니라 재할당된 값의 주소로 참조를 변경하는 것이다.

이런 특성을 **불변성** 이라고 한다.

이때, 문자열 또한 원시값으로 분류된다.
하지만, 문자열은 유사 배열 객체이면서 이터러블이므로 배열과 유사하게 문자에 접근할 수 있다.

#### 1-1. 값에 의한 전달

```javascript
var score = 80;
var copy = score;

console.log(score); // 80
console.log(copy); // 80

score = 100;

console.log(score); // 100
console.log(copy); // 80
```

변수에 원시 값을 갖는 변수를 할당하면 할당받는 변수에는 할당되는 변수의 원시 값이 복사되어 전달된다. 이를 **값에 의한 전달**이라고 한다.

![img](https://velog.velcdn.com/images%2Fniyu%2Fpost%2F43043885-ad53-4e57-96fc-bc816075cc70%2F66475024-76923780-eacd-11e9-92ff-0ba267df2d44.jpeg)

변수에 원시 값을 갖는 변수를 할당하면 값은 동일하게 갖지만 값이 같다고 주소까지 같지는 않다.

따라서 score 변수의 값을 변경해도 copy 변수의 값에는 어떤 영향도 주지 않는다.

### 2. 객체

> 객체는 프로퍼티의 개수가 정해져 있지 않으며, 동적으로 추가/삭제할 수 있다.
> 또한 프로퍼티의 값에도 제약이 없다.
>
> 즉, 원시 갑소가 같이 확보해야 할 메모리 공간의 크기를 사전에 정해 둘 수 없다.

#### 2-1 변경 가능한 값

객체(참조) 타입의 값, 즉 객체는 변경 가능한 값이다.

원시 값과 달리 객체를 할당한 변수가 기억하는 메모리 주소를 통해 메모리 공간에 접근하면 **참조 값**에 접근할 수 있다.

변경이 불가능한 원시 값과 달리 객체는 변수의 재할당 없이 객체를 직접 변경할 수 있다.
즉, 프로퍼티를 동적으로 추가, 갱신, 삭제할 수 있다.

#### 2-2 참조에 의한 전달

객체를 가리키는 변수를 다른 변수에 할당하면 원본의 참조 값이 복사되어 전달 된다.
이를 **참조에 의한 전달**이라 한다.

![img](https://velog.velcdn.com/images%2Fniyu%2Fpost%2F4a546bbe-aad5-4285-a514-65f77e2517c3%2F2021-06-24%2019%3B34%3B27.PNG)

위 그림처럼 원본 person을 사본 copy에 할당하면 원본 person의 참조 값을 복사해서 copy에 저장한다. 이때 원본 person과 사본 copy는 저장된 메모리 주소는 다르지만 동일한 참조 값을 갖는다.

즉, 두 개의 식별자가 하나의 객체를 공유한다.
**따라서 어느 한쪽에서 객체를 변경하면 서로 영향을 주고 받는다.**



값에 의한 전달과 참조에 의한 전달은 식별자가 기억하는 메모리 공간에 저장되어 있는 값을 복사해서 전달한다는 면에서 동일하다.
차이는 변수에 저장된 값이 원시 값인지 참조 값인지 차이가 있을 뿐이다.



### 얕은 복사와 깊은 복사

객체를 프로퍼티 값으로 갖는 객체의 경우 얕은 복사는 한 단계까지만 복사하는 것을 말하고 깊은 복사는 객체에 중첩되어 있는 객체까지 모두 복사하는 것을 말한다.

```javascript
const o = { x: {y : 1} };

//얕은 복사
const c1 = { ...o };
console.log(c1 === o);     //false
console.log(c1.x === o.x); //true

//lodash의 cloneDeep을 사용한 깊은 복사
const _ = require('lodash');

//깊은 복사
const c2 = _.cloneDeep(o);
console.log(c2 === o);     //false
console.log(c2.x === o.x); //false
```

얕은 복사와 깊은 복사로 생성된 객체는 원본과는 다른 객체다. 즉, 원본과 복사본은 참조 값이 다른 별개의 객체다. 
하지만 얕은 복사는 객체에 중첩되어 있는 객체의 경우 참조 값을 복사하고 깊은 복사는 객체에 중첩되어 있는 객체까지 모두 복사해서 원시 값처럼 완전한 복사본을 만든다.

또한 원시 값을 할당한 변수를 다른 변수에 할당하는 것을 깊은 복사.
객체를 할당한 변수를 다른 변수에 할당하는 것을 얕은 복사라고 하기도 한다.