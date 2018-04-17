---
layout: post
title: Javascript 의 arguments
categories: [frontend]
---

arguments는 배열처럼 보이지만 배열은 아닌 함수의 지역변수이다. 

함수가 실행되면 arguments가 생성된다. 

```js

function a(){
    console.log(arguments);
    console.log(arguements.length);
}
a(1,2,3,4); //[ 1,2,3,4, callee: ƒ, Symbol(Symbol.iterator): ƒ ]  , 4

a(); // [callee: ƒ, Symbol(Symbol.iterator): ƒ] , 0

```
arguments는 배열은 아니지만 length 프로퍼티를 가지고 있는 object다. 

따라서 arguments는 pop메소드를 가지고 있지 않다. 그러나 array처럼 만들어줄 수 있다. 

```js

var args = [ ...arguments];

a(1,2,3,4); // [1,2,3,4];

```

위와 같이 es6문법에서 등장한 전개 연산자를 이용해서 배열로 만들어줄 수 있고,

```js
var args = Array.prototype.slice.call(arguments);

a(1,2,3); //[1,2,3];

```

slice메소드로 배열로 만들어줄 수 있다.

그러나 자바스크립트엔진 최적화에 있어서 기피된다. 

arguments 속성으로는

arguments.callee : 현재 실행중인 함수를 가리킨다.
arguments.caller : 현재 실행중인 함수를 호출한 함수를 가리킨다.
arguments.length가 있다. 