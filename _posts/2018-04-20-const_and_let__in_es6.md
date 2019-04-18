---
layout: post
title: es6에서 추가된 const 와 let
categories: [frontend]
---
Es6에서는 const와 let이 추가된다.  

### let 

변수가 가진 중요한 특징은 변수의 자료형, 변수형, 생명주기가 있다. 

let은 es5의 변수 var와 다른데, 중괄호 안이 변수의 스코프이기 때문이다. 

es6는 블럭 스코프이자 렉시컬 스코프이다. 

렉시컬 스코프는 자바스크립트가 기존에 가지던 특징이다. 

렉시컬 스코프란, 함수가 선언되는 순간, 함수가 선언된 환경에서의 변수를 참조하게 된다는 것을 뜻한다.

예시로 자바스크립트는 클로저를 가지고 있다. 

클로저는 함수가 실행된 순간 <u>함수가 정의된 환경</u>으로 '참조'한다.

함수를 처음 선언하는 순간, 함수 내부의 변수는 자기 스코프로부터 가장 가까운 곳에 있는 변수를 계속 참조하게 된다. 
 
클로저는 for문 안에 들어있는 변수를 참조하는데, 그것은 스택에 쌓이는 값이고 주소를 들고 있지 않다. 

let 변수가 var 변수와 클로저에서 다른 결과를 보여주는 것은 

클로저 내에서 값을 클론한 주소를 가지고 있기 때문이다. 따라서 스택의 값이 변경되는 게 아니라 클론한 값(새로 생긴 주소값)이 생성된다.


<br/>
<br/>
<br/>

### const

const는 변수가 아니라 상수다. 

상수라는 것은 변경될 수 없는 걊이다. 

객체가 상수가 될 수 있는가? 될 수 있다. 

객체의 프로퍼티도 변경되고 삭제/추가 될 수 있으며 객체는 변경될 수 있다.

[스택과 힙](http://estrella-kim.github.io/stack_and_heap)의 메모리에서 생각해보면 당연하다. 
 
스택은 크기와 시작위치를 알 수 있기 때문에 값 자체를 가지고 있는다. 

하지만 객체는 힙에 쌓이는데 힙은 크기와 위치를 모르기 때문에 주소값을 준다. 

즉 const에 객체가 올 때 객체에 변동이 있더라도 주소값은 변동되지 않기 때문에 상수이다.