---
layout: post
title: 객체와 원시객체와 null과 undefined
categories: [frontend]
---

C언어에서는 number, string이 객체로 존재한다. 

어느정도 C언어를 기반으로 만들어진 javascript에서 기존 언어들의 개념으로 생각해보면, 수(number)와 문자열(string)은 수많은 객체들 중에 존재한다고 이해할 수도 있다. 

그러나 자바스크립트에서는 수와 문자열을 원시객체로써 받아들인다. 

또한 수와 문자열 뿐 아니라 null과 boolean, undefined 도 원시객체이다.
 
(주의할 점은, 자바스크립트라는 언어에서만 그렇다는 점이다.)

### NULL

null은 크기가 정해진 그릇에 아무것도 담고 있지 않는다는 의미를 지니고 있다. 그런데 컴퓨터는 사실 아무것도 담겨 있지 않은 그릇이라는 개념을 받아들이지 않는다. 그렇기 때문에 보이지는 않지만 null이 가진 그릇 안에는 0이 담겨있다. 그리고 null이이 가진 메모리에는 '아무것도 담겨있자않아요'가 담겨있다. 

### null 에 대한 논란

```js
console.log(typeof null); //object 
```
 콘솔로 찍어보면 null의 타입은 객체다. 
 
 국내에서도 대다수 블로그에서나 해외의 stackoverflow를 찾아보면 이는 javascript의 오류라고 말하고 있다. 
 
 그러나 이번에 스터디에서 강의를 해주신 분은 이렇게 말씀했다.

"null이 object인 것은 오류가 아니다. 만일 오류였다면 ECMA6에서 고쳐졌을 것이다. "

이에 대해서 곧 null도 보이지 않는 무언가를 담고 있는 객체라는 것이고, 객체이지만 '아무것도 담고 있지않다'라는 약속을 지닌 원시객체로 구분했다는 의미로 받아들였다. 

### undefined

컴퓨터는 크기가 정해지지 않고, 애매모호한 것을 싫어한다. 

애매모호한 것은 없는 것으로 치부한다. 

여기서 undefined는 그릇도 정해지지않고(크기가 정해지지않고) 안에 담긴 것도 없는 애매모한 상태이다. 

여기서 의문 한가지 ! 

undefined 와 undefined 를 +연산자로 연산시에는 결과값이  NaN이 도출된다. 

단어의 뜻으로만 보면  not a number라는 결과는 맞다. 

그러나 not a number의 type 은 number이다. 


```js

function test(a,b){
    return a +b;
}
test(undefined, undefined); //NaN

```
not a number를 생성하는 방식이 메모리에 담기지 못할 만큼 큰 숫자를 넣을 때 오류가 뜨는 방식이라면, NAN의 type은 number이다. 

이 흐름이라면 undefined는 그릇도 값도 정해지지 않았기 때문에 number type이라고 정의내릴 수 없다. 

따라서 undefined+undefined는 return 값이 undefined 로 나와야한다고 생각했다. 

의문에 대해서 여러가지 가정을 해보자면,

```js

undefined +1; //NaN

undefined + false //NaN

undefined + null //NaN

null + null // 0

undefined + "string"; // "undefinedstring"

```

undefined를 연산했을 때, string을 제외한 type에서 암묵적 형변환을 함으로써 NaN이라는 number type으로 변환된다. 

따라서 undefined + undefined = NaN + NaN 이므로 NaN이 도출된다.


