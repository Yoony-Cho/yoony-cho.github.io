---
date: 2022-12-10T00:30:05.000Z
layout: post
published: true
title: "[JavaScript] Control flow statement"
subtitle: What is Control flow statement?
description: Let's find out the type of control flow statement
image: https://cdn.pimylifeup.com/wp-content/uploads/2022/04/javascript-for-loops-Thumbnail-NoWM.png
optimized_image: https://cdn.pimylifeup.com/wp-content/uploads/2022/04/javascript-for-loops-Thumbnail-NoWM.png
category: JAVASCRIPT
tags:
  - JS
  - CS
  - Code
author: yoony
---

## What is Control flow statement?

> 일반적으로 Top - Down 방식으로 순차적으로 실행되는 코드를 조건, 반복문 등을 통해 흐름을 인위적으로 제어할 수 있다.
> 다만, 제어문은 코드의 흐름을 이해하기 어렵게 만들어 가독성을 해치는 단점이 있다.



## 블록문

0개 이상의 문을 중괄호로 묶은 것으로, 코드 블록 또는 블록이라고 부른다.
자바스크립트의 블록문은 하나의 실행 단위로 취급된다.



## 조건문

### 1. if ... else 문

주어진 조건(불리언 값으로 평가될 수 있는 표현식)의 평가 결과로 실행할 코드블록을 결정한다.

```javascript
if (조건식 1) {
  //조건식 1이 참이면 이 코드블록이 실행
} else if (조건식 2) {
  //조건식 2가 참이면 이 코드블록이 실행
} else {
  //둘 다 참이 아니면 이 코드블록이 실행
}
  
```

대부분의 if ... else문은 삼함 조건 연산자로 변경이 가능하다.

### 2. Switch문

주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는  case 문으로 실행 흐름을 옮긴다.
만약 표현식과 일치하는 case가 없다면 실행 순서는 default문으로 이동한다.

``` javascript
switch (표현식) {
  case 표현식1:
    switch문의 표현식과 표현식 1이 일치하면 실행될 문;
    break;
  case 표현식2:
    switch문의 표현식과 표현식 2가 일치하면 실행될 문;
    break;
  default:
    switch문의 표현식과 일치하는 case가 없을 때 실행될 문;
}
```

불리언 값으로 평가되는 if ...else와는 조금 다르게 switch문은 문자열이나 숫자 값을 평가하는 경우가 많다.

## 반복문

조건식의 평가 결과가 참인 경우 코드 블록을 실행한다.
그 후 조건식을 다시 평가하여 조건식이 거짓일 때까지 코드 블록을 다시 실행한다.

> 반복문을 대체할 수 있는 기능으로는 forEach 메소드, for ...in 문, for ...of문 등이 있다.

### 1. for 문

조건식이 거짓으로 평가될 때 까지 코드 블록을 반복 실행한다.

``` javascript
for (변수 선언문 또는 할당문; 조건식; 증감식){
	조건이 참인경우 반복 실행될 문;
}
```

### 2. while 문

주어진 조건식의 평가 결과가 참이면 코드 블록을 계속 반복한다 for문과 비슷하지만 for문은 반복 횟수가 확실할 때 사용하고 while은 반대의 경우 주로 사용한다.

```javascript
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 반복 실행한다
while (count < 3){
  console.log(count); // 0 1 2
  count++;
}
```

### 3. do ...while문

코드 블록을 무조건 한번 이상 실행하고 조건식을 평가하여 반복 실행한다.

``` javascript
var count = 0;
// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
do {
  console.log(count); // 0 1 2
  count++;
} while(count < 3);
```

### 4. Break 문

코드 블록을 탈출할 때 사용하는 문으로 조금 더 정확하게는 코드 블록이 아닌 레이블 문, 반복문, switch문의 코드 블록을 탈출한다.
그 외에 사용 시 문법에러가 발생한다.

### 5. Continue 문

반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동 시킨다. break처럼 탈출하지 않는다.

```javascript
for (let i = 0; i < string.length; i++){
  if (string[i] !== search) continue;
  count++;
}
```

이때 continue를 사용하면 if문 밖에 코드를 작성 할 수 있다.