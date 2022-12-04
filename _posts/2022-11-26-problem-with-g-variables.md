---
date: 2022-11-26T00:30:05.000Z
layout: post
title: "[JavaScript] Problems with global variables"
subtitle: Problems with global variables
description: Let's find out what's wrong with global variables
image: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQJWwnhSs2ijPwEPHfcIkqlwLkFeFqmG01aLxAt5qeodBqRcxG2jAoScVjMVQHpkbjuXIw&usqp=CAU
optimized_image: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQJWwnhSs2ijPwEPHfcIkqlwLkFeFqmG01aLxAt5qeodBqRcxG2jAoScVjMVQHpkbjuXIw&usqp=CAU
category: JAVASCRIPT
tags:
  - JS
  - CS
  - Code
author: yoony
---

## Problems with global variables

### 1. 변수의 생명주기

> 전역변수의 무분별한 사용은 위험하다.
> 전역 변수를 반드시 사용해야 할 이유를 찾지 못한다면 지역 변수를 사용해야 한다.

#### 1-1 지역 변수의 생명주기

변수는 선언에 의해 생성되고 할당을 통해 값을 갖는다. 그리고 언젠가 소멸하는 생성, 소멸의 생명주기를 갖는다.

변수는 자신이 선언된 위치에서 생성, 소멸된다.
**전역 변수**의 경우는 **애플리케이션의** 실행과 종료가 **생명주기와 동일**하지만 함수 내부에 선언된 **지역 변수**는 **함수의** 호출과 종료가 **생명주기와 동일**하다.

```javascript
function alpha(){
  var x = 'hello world';
  console.log(x); // local
  return x;
}

alpha();
console.log(x); //ReferenceError: x is not defined
```

지역 변수인 x는 alpha 함수가 호출되기 전까지는 생성되지 않는다. 
alpha함수를 호출하지 않으면 함수 내부의 변수 선언문이 실행되지 않기 때문이다.

***여기서 호이스팅의 개념이 들어와 혼돈될 수 있다.**
호이스팅 동작으로인해 변수는 모두 선언문의 위치와 상관없이 일단 선언이 되고 시작하는거 아닌가?

**위 내용은 전역 변수에 한정된 내용이다.**

함수 내부에서 선언된 변수는 함수가 호출된 직후 선언되며 함수 내부 코드가 순차적으로 실행된다.
이후 함수가 종료됨에 따라 변수 또한 소멸되어 생명 주기가 종료된다.

```javascript
function alpha() { //함수 선언
  //변수 x 생성
  var x = 'hello world'; //값 할당
  console.log(x);
  return x;
  //변수 x 소멸
}

alpha();
console.log(x); //ReferenceError: x is not defined
```

단, 누군가 함수가 생성한 스코프를 참조하고 있다면 함수가 종료된 이후에도 스코프는 소멸하지 않고 남아있어 지역 변수도 함수 종료와 함께 소멸하지 않고 남아 있을 수 있다.
자세한 내용은 **클로저**를 공부하자



#### 1-2 전역 변수의 생명 주기

> 전역변수는 명시적인 호출 없이 실행, 즉 코드가 로드되는 순간 실행된다.
> 마찬가지로 종료 또한 마지막 문이 실행되어 더 이상 실행할 문이 없으면 종료한다.

var 키워드로 선언한 전역 변수의 경우 전역 객체의 프로퍼티가 된다.
이는 전역 객체의 생명주기와 전역 변수의 생명주기가 같음을 의미한다.

> 전역 객체란 코드가 실행되기 이전 JS 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체로 클라이언트 사이드 환경 즉 브라우저에서는 window, 서버 사이드 환경에서는 global 객체를 의미한다.
> 전역 객체는 window, self, this, frames, global 등 다양한 식별자가 존재했지만 ES11에서 globalThis로 통일 되었다.

브라우저 환경에서 전역 객체는 window이므로 var키워드로 선언된 전역 변수는 window의 프로퍼티다.
window는 웹페이지를 닫기 전까지 유효하다.

### 2. 전역 변수의 문제점

**1) 암묵적 결합**
모든 코드가 전역 변수를 참조하고 변경할 수 있도록 허용하는 것을 암묵적 결합이라고 하고 이는 변수의 유효 범위가 클수록 나빠지는 가독성과 의도치 않은 상태 변경에 위험이 있다.

**2) 긴 생명 주기**
전역 변수는 생명주기가 길기 때문에 메모리 리소스 또한 오래 소비된다. 

**3) 스코프 체인상에서 종점에 존재**
전역 변수는 스코프상 마지막까지 남아있다 즉, 변수를 검색할 때 전역변수가 가장 마지막에 검색된다는 의미이다. 검색 속도는 차이가 크지 않지만, 속도의 차이는 분명히 있다.

**4) 네임스페이스 오염**
JS의 문제점 중 하나는 파일이 분리되어 있어도 전역 스코프는 하나를 공유한다는 것이다.
따라서 다른 파일에서 동일한 이름의 전역 변수나 전역 함수가 같은 스코프 내에 존재할 때 예상치 못한 문제를 야기할 수 있다.

### 3. 전역 변수의 사용을 억제하는 방법

> 전역 변수의 무분별한 사용은 위험하다.
> 전역 변수를 반드시 사용해야 할 이유를 찾지 못한다면 지역 변수를 사용해야 한다.
> 변수의 스코프는 좁을수록 좋다.

**1) 즉시 실행 함수**
함수 정의와 동시에 호출되는 즉시 실행 함수는 단 한 번만 호출되는데 모든 코드를 즉시 실행 함수로 감싸면 모든 변수는 즉시 실행 함수의 지역 변수가 된다 이런 특성을 이용해 전역 변수의 사용을 제한한다.

```javascript
(function () {
  var x = 10; // 즉시 실행 함수의 지역 변수
}());
console.log(x); // ReferenceError: x is not defined
```



**2) 네임스페이스 객체**
전역에 네임스페이스 역할을 담당할 객체를 생성하고 전역 변수처럼 사용하고 싶은 변수를 프로퍼티로 추가하는 개념

```javascript
var MYAPP = {}; //전역 네임스페이스 객체

MYAPP.person = {
  family-name: 'Cho'
  given-name: 'BY'
};

console.log(MYAPP.person.family-name); // Cho
```

다만, 이 방법은 식별자 충돌을 방지할 수는 있으나 어쨌든 네임스페이스 객체 자체가 전역 변수에 할당되므로 유용한 방법은 아니다.

**3) 모듈 패턴**
이 방법은 클래스를 모방해서 관련있는 변수와 함수를 모아 즉시 실행 함수로 감싸 하나의 모듈화를 시키는 작업으로 클로저를 기반으로 동작한다.
모듈 패턴는 전역 변수의 억제는 물론 캡슐화까지 구현 가능하다.

```javascript
var Counter = (function(){
  var num = 0; //즉시 실행 함수의 지역 변수이자 private 변수
  
  return {
    increase(){
      return ++num;
    },
    decrease(){
      return --num;
    }
  };
}());

console.log(num); // undefined (private변수는 외부 노출 되지 않음)

console.log(increase()); // 1
console.log(increase()); // 2
console.log(decrease()); // 1
console.log(decrease()); // 0
```

즉시 실행 함수는 객체를 반환하고 이 객체에는 외부에 노출시키고 싶은 변수나 함수를 담아 반환한다.
반대로 외부에 노출하고 싶지 않은 변수나 함수는 객체에 추가하지 않으면 외부에서 접근할 수 없다.

> 캡슐화 : 객체의 상태를 나타내는 프로퍼티와 프로퍼티를 참조하고 조작할 수 있는 메서드라는 동작을 하나로 묶는 것
>
> 클로저: 클로저는 반환된 내부함수가 자신이 선언됐을 때의 환경(Lexical environment)인 스코프를 기억하여 자신이 선언됐을 때의 환경(스코프) 밖에서 호출되어도 그 환경(스코프)에 접근할 수 있는 함수를 말한다.
> 즉, **자신이 생성될 때의 환경을 기억하는 함수**

**4) ES6 모듈**

ES6 모듈은 파일 자체의 독자적인 모듈 스코프를 제공하므로 전역 변수를 사용할 수 없다.
따라서 모듈 내 var 키워드로 선언한 변수는 더는 전역 변수도 window 객체의 프로퍼티도 아니다.

모듈 파일의 확장자는 mjs를 권장하고 사용방법은 script 태그에 type="module" 어트리뷰트를 추가해주면 로드된 자바스크립트 파일은 모듈로 동작한다.

```javascript
<script type="module" src="lib.mjs"></script>
<script type="module" src="app.mjs"></script>
```





