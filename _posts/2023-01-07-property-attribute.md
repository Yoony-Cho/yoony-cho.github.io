---
date: 2023-01-07T00:30:05.000Z
layout: post
published: true
title: "[JavaScript] Property Attribute"
subtitle: What is a Property Attribute?
description: Let's find out the Property Attribute in JavaScript
image: https://velog.velcdn.com/images/yena1025/post/194d172d-1e7f-4a33-9cb5-5c861479cf3b/image.jpg
optimized_image: https://velog.velcdn.com/images/yena1025/post/194d172d-1e7f-4a33-9cb5-5c861479cf3b/image.jpg
category: JAVASCRIPT
tags:
  - JS
  - CS
  - Code
author: yoony
---

## What is a Property Attribute?

> **자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다**

## 내부 슬롯과 내부 메서드

>  내부 슬롯과 내부 메서드란, 자바스크립트 엔진의 구현 알고리즘을 설명하기 위해 ECMAScript 사양에서 사용하는 의사 프로퍼티(pseudo property)와 의사 메서드(psuedo method)다.

내부 슬롯과 내부 메서드는 ECMAScript 사양에 정의된 대로 구현되어 엔진 내에 실제로 동작하지만 개발자가 직접 접근할 수는 없다.

단 일부 내부 슬롯과 메서드에 한해 간접 접근이 가능한데 [[Prototype]]이라는 내부 슬롯을가져 proto를 통해 간접 접근할 수 있다.

```
const o = {};

// 내부 슬롯은 자바스크립트 엔진의 내부 로직이므로 직접 접근할 수 없다.
o.[[Prototype]]; // Uncauhgt SyntaxError: Unexpected token '['
// 단, 일부 내부 슬롯과 메서드에 한하여 간접적으로 접근할 수 있는 수단을 제공한다.
o.__proto__
```

# 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체

> **자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.** 

- 프로퍼티 상태란, **프로퍼티 값(value)**, **값의 갱신 가능 여부(writable)**, **열거 가능 여부(enumerable)**, **재정의 가능 여부(configurable)**를 말한다.
- 각각 내부 슬롯 [[Value]], [[Writable]], [[Enumerable]]. [[Configurable]]을 간접적으로 확인할 수 있다.

```
const person = {
  name: "Seo",
}

// 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체를 반환한다.
console.log(Object.getOwnPropertyDescriptor(person, "name"))

// {value: 'Seo', writable: true, enumerable: true, configurable: true};
```

- 첫 번째 매개변수에는 **객체의 참조**를 전달하고, 두 번째 매개변수에는 **프로퍼티 키**를 문자열로 전달한다. (존재하지 않으면 undefined)
- Object.getOwnPropertyDescriptor 메서드는 하나의 프로퍼티에 대해 프로퍼티 디스크립터 객체를 반환하지만, ES8에서 도입된 Object.getOwnPropertyDescriptors 메서드는 모든 프로퍼티의 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체들을 반환한다.

```
const person = {
  name: "Seo",
}

// 프로퍼티 동적 생성
person.age = 20

// 모든 프로퍼티의 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체들을 반환한다.
console.log(Object.getOwnPropertyDescriptors(person))
```

# 데이터 프로퍼티와 접근자 프로퍼티

####1. 데이터 프로퍼티

- 키와 값으로 구성된 일반적인 프로퍼티다.


- 데이터 프로퍼티가 같은 어트리뷰트는 다음과 같다.
  - 이 어트리뷰트는 자바스크립트 엔진이 프로퍼티를 생성할 때 기본값으로 정의된다.

####2. 접근자 프로퍼티

- 접근자 프로퍼티(Accessor property)는 자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수로 구성된 프로퍼티다.

**메서드 앞에 get, set이 붙은 메서드가 getter, setter 함수이고, 함수 이름이 접근자 프로퍼티가 된다.**

접근자 프로퍼티는 자체적으로 값을 가지지 않으며, 데이터 프로퍼티의 값을 읽거나 저장할 때 관여할 뿐이다.

## 프로토타입(prototype)

- **프로토타입**은 어떤 객체의 상위(부모) 객체의 역할을 하는 객체다.
- 프로토타입은 **하위(자식) 객체에게 자신의 프로퍼티와 메서드를 상속**한다.
- 프로토타입 객체의 프로퍼티나 메서드를 상속받은 하위 객체는 자신의 프로퍼티 또는 메서드인 것처럼 자유롭게 사용할 수 있다.
- **프로토타입 체인**은 프로토타입이 단반향 링크드 리스트 형태로 연결되어 있는 상속 구조를 말한다.
- 객체의 프로퍼티나 메서드에 접근하려고 할 때, 해당 객체에 접근하려는 프로퍼티 또는 메서드가 없다면 프로토타입 체인을 따라 프로토타입의 프로퍼티나 메서드를 차례대로 검색한다.
- 접근자 프로퍼티와 데이터 프로퍼티를 구별하는 방법은 다음과 같다.

```
// 일반 객체의 __proto__는 접근자 프로퍼티다.
Object.getOwnPropertyDescriptor(Object.prototype, "__proto__")
// {get: f, set: f, enumerable: false, configurable: true};

Object.getOwnPropertyDescriptor(function () {}, "prototype")
// {value: {...}, writable: true, enumerable: false, configurable: false}

//Object.getOwnPropertyDescriptor를 통해 반환된 어트리뷰트 객체를 보면 다르다는 것을 알 수 있다.
```

## 프로퍼티 정의

- **프로퍼티 정의**란 새로운 프로퍼티를 추가하면서 **프로퍼티 어트리뷰트를 명시적으로 정의**하거나, 기존 프로퍼티의 프로퍼티 어트리뷰트를 **재정의**하는 것을 말한다.
- Object.definedProperty 메서드를 사용하면 프로퍼티의 어트리뷰트를 정의할 수 있다.


- Object.defineProperty 메서드로 프로퍼티를 정의할 때 프로퍼티 디스크립터 객체의 프로퍼티를 일부 생략할 수 있으며, 생략된 어트리뷰트는 다음과 같이 기본값이 적용된다.
  - value : undefined
  - get : undefined
  - set : undefined
  - writable : false
  - enumerable : false
  - configurable : false
- Object.definedProperty 메서드는 한번에 하나의 프로퍼티만 적용 가능하며, Object.definedProperties 메서드를 사용하면 여러 개 프로퍼티를 한 번에 정의할 수 있다.

## 객체 변경 방지

- 객체는 변경 가능한 값이므로 재할당 없이 직접 변경할 수 있다.
- Object.defineProperty 또는 Object.definedProperties 메서드를 사용해 프로퍼티 어트리뷰트를 재정의할 수도 있다.

### 1. 객체 확장 금지

- Object.preventExtensions 메서드는 객체의 확장을 금지(프로퍼티 추가 금지)한다.
  - **확장이 금지된 객체는 프로퍼티 추가가 금지된다**.
  - 프로퍼티는 프로퍼티 동적 추가와 Object.defineProperty 메서드로 추가할 수 있는데 두 가지 방법이 모두 금지된다.
- 확장이 가능한 객체인지 여부는 Object.isExtensible 메서드로 확인할 수 있다.

###  2. 객체 밀봉

- Object.seal 메서드는 객체를 밀봉한다. **밀봉이란 프로퍼티 추가 및 삭제와 프로퍼티 어트리뷰트 재정의 금지를 의미한다.**
- **밀봉된 객체는 읽기와 쓰기만 가능하다.**
- 밀봉 객체인지 여부는 **Object.iseSealed** 메서드로 확인할 수 있다.

### 3. 객체 동결

- Object.freeze 메서드는 객체를 동결한다. **동결**이란, **프로퍼티 추가 및 삭제와 프로퍼티 어트리뷰트 재정의 금지, 프로퍼티 값 갱신 금지를 의미한다.**
- **동결된 객체는 읽기만 가능하다.**
- 동결된 객체인지 여부는 **Object.isFrozen** 메서드로 확인할 수 있다.

### 4 불변 객체

- 위의 변경 방지 메서드들은 얕은 변경 방지(shallow only)로 직속 프로퍼티 변경만 방지되고 중첩 객체까지는 영향을 주지 못한다.
- Object.freeze 메서드로 객체를 동결하여도 중첩 객체까지 동결할 수는 없다.

