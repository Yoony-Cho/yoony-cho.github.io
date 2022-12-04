---
date: 2022-11-27T00:30:05.000Z
layout: post
title: "[JavaScript] Variable Keywords"
subtitle: Variable Keywords
description: Characteristics and differences of variable keywords
image: https://res.cloudinary.com/practicaldev/image/fetch/s--wWLfMCjV--/c_imagga_scale,f_auto,fl_progressive,h_500,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/i/gos81vmdo7fel8r8yi8l.jpg
optimized_image: https://res.cloudinary.com/practicaldev/image/fetch/s--wWLfMCjV--/c_imagga_scale,f_auto,fl_progressive,h_500,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/i/gos81vmdo7fel8r8yi8l.jpg
category: JAVASCRIPT
tags:
  - JS
  - CS
  - Code
author: yoony
---

## Variable Keywords and Block level scope

### 1. Var

> ES5까지 변수는 var키워드 만을 사용하여 선언할 수 있었다.
> var키워드가 가지고 있는 문제점을 알아보자

#### 변수 중복 선언 허용

var키워드로 선언한 변수는 중복 선언이 가능하다

```js
var x = 1;
var y = 1;

var x = 100;
var y;

console.log(x); // 100
console.log(y); // 1
```

이렇게 var키워드로 선언된 변수는 같은 스코프 내에서 중복선언이 가능하고 런타임에 의해 마지막에 할당한 값으로 값이 변하게 된다.

다만 ```var y;```처럼 초기화 문이 없으면 변수 선언은 무시된다.

#### 함수 레벨 스코프

var키워드로 선언한 변수는 오직 함수 코드 블록에서만 지역 스코프를 인정하고 그 외 상황은 모두 전역 변수가 된다.

```javascript
var x = 1;

if (true){
  var x= 10;
}

console.log(x); // 10 

//함수가 아닌 if문에서 var로 중복 선언하였기 때문에 
//전역 변수가 되어 if문 밖에서 참조한 x값이 10으로 변경
```

#### 변수 호이스팅

> var 키워드로 변수를 선언하면 변수 호이스팅에 의해 변수 선언문이 스코프 맨 위로 끌어 올려진 것 처럼 동작한다. 
> 즉 var키워드로 선언한 변수는 변수 선언문 이전에 참조가 이루어 질 수 있다.

```javascript
console.log(x); // undefined 
//var는 선언과 동시에 undefined로 초기화 됨

x = 1; // 변수에 값 할당

console.log(x); // 1 
//값 할당이 이루어진 후에 순차적으로 진행된 참조는 할당값을 출력한다.

var x; // 변수 선언
```



### 2. Let

> ES6에서 const와 함께 let 키워드가 변수 선언 키워드로 추가됨.
> var와 let의 차이점이 무엇인지 알아보자

#### 변수 중복 선언 금지

var 키워드와 달리 let은 변수를 중복 선언 할 수 없다.

```javascript
let x = 123;
let x = 456; //SyntaxError: Identifier 'x' has already been declared
```



#### 블록 레벨 스코프

var 키워드에서는 함수 코드 블록만 지역 스코프로 인정했으나 let은 모든 코드 블록을 지역 스코프로 인정하는 블록 레벨 스코프를 따른다.

```javascript
//전역 스코프
let x = 1;
//함수 레벨 스코프
function y() {
  let x = 100;
  let y = 200;
  //블록 레벨 스코프
  for(let x = 1; x < 3; x++){
    console.log(x); // 1, 2
  }
  //함수 레벨 스코프
  console.log(x); // 100
}
//전역 스코프
y();
console.log(x); // 1
console.log(y); // ReferenceError: y is not defined
```

여기서 { } 이런 코드 블럭 안에 있는 모든 let 변수 선언은 지역 변수이다 따라서 코드 블럭 밖에서 참조를 하게 되면 참조 에러를 발생시키게 된다.

#### 변수 호이스팅

> var와 달리 let은 변수 호이스팅이 발생은 하지만 발생하지 않는 것처럼 보인다.

```javascript
console.log(x); // ReferenceError: x is not defined
let x;
```

이는 선언과 동시에 undefined로 초기화 하는 var와 달리 let은 선언과 초기화가 분리되어 진행되기 때문이다. 
따라서 초기화 이전에 변수에 접근하려했기 때문에 참조 에러가 발생한다.

그러나 그렇다고 호이스팅이 되지 않는것은 아니다.

```javascript
let x = 1 //전역 변수
{
  console.log(x); // ReferenceError: Cannot access 'x' before initialization
  let x = 2;
}
```

위의 결과는 let으로 선언한 x변수가 호이스팅 되었다는 것을 알 수 있다.
만약 x가 호이스팅 되지 않았다면 전역 변수 x의 값인 1을 출력했어야 하나 지역 변수 x가 호이스팅 되었기 때문에 여전히 참조 에러가 발생하게 된다.

```Html
자바스크립트는 ES6에서 도입된 let, const를 포함 모든 선언을 호이스팅한다.
다만 ES6에서 도입된 let, const, class를 사용한 선언은
호이스팅이 발생하지 않는 것처럼 동작한다.
```



### 3. Const

> const는 constant에서 가져온 키워드인 만큼 상수를 선언하는데 주로 사용한다. 
> let과 함께 ES6에서 추가된 개념으로 비슷하지만 차이가 있는 let과 비교해보자

#### 선언과 초기화

let과 달리 const 는 선언과 동시에 초기화하는 문법을 사용해야 한다.

```javascript
const x = 1;
const y; // SyntaxError: Missing initializer in const declaration
```

그렇지 않으면 위 결과처럼 문법에러가 발생하게 된다.

#### 재할당 금지

var와 let으로 선언한 변수는 재할당이 가능하지만 const는 재할당이 불가능하다.
이러한 이유로 const를 상수 선언에 사용하게된다.

```javascript
const x = 1;
x = 2; // TypeError: Assignment to constant variable
```

#### 상수

사실상 위에서 설명한 재할당과 같은 의미라고 볼 수 있다.
const로 선언한 변수에 원시값을 할당하면 재할당 없이 값을 변경할 수 없는데 const는 재할당이 불가능하므로 변하지 않는 상수가 된다.

상수는 상태 유지와 가독성, 유지보수의 편의를 위해 적극 사용되어야 한다.

```javascript
//상수 사용 전
let preTaxPrice = 100; // 세전

let afterTaxPrice = preTaxPrice + (preTaxPrice * 0.1) // 세후

//상수 사용 시
const Tax_Rate = 0.1 // 대문자를 활용해 상수임을 확실하게 표현

let preTaxPrice = 100; // 세전

let afterTaxPrice = preTaxPrice + (preTaxPrice * Tax_Rate) // 세후

```

0.1이라는 변하지 않는 수를 상수로 표현한다.



#### const 키워드와 객체

const 키워드로 선언된 변수는 원시 값을 할당할 경우 값 변경이 불가능하다.
다만, 원시 값이 아닌 객체를 할당한 경우에는 값 변경이 가능하다.
객체의 경우 재할당 없이도 직접 변경이 가능하기 때문이다.

```javascript
const person = {
  name: 'Cho'
};
person.name = 'BY';
console.log(person); // {name:'BY'}
```

위 결과에서 확인할 수 있는 내용은 const는 재할당을 금지할 뿐 **불변**을 의미하지는 않는다는 점이다.

> 변수 선언은 기본적으로 **const**를 사용하고 재할당이 필요한 경우에 let을 사용한다.
> const를 사용하면 의도치 않은 재할당을 방지하기 때문에 좀 더 안전하다. 

#### 변수 선언시 권장사항

> - ES6 사용시 var키워드는 사용하지 않는다.
> - 재할당이 필요한 경우 let을 사용한다. (이때 변수 스코프는 최대한 좁게 만든다)
> - 변경이 발생하지 않고 읽기 전용으로 사용하는(상수) 원시 값과 객체에는 const 를 사용한다. const 키워드는 var와 let보다 안전하다.



