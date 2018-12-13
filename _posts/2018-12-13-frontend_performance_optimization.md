---
layout: post
title: 프론트엔드 성능최적화
categories: [frontend]
---

#프런트엔드 성능 최적화

프론트엔드 성능을 최적화하는 방법을 크게 두 가지 로딩최적화, 렌더링 최적화로 나눌 수 있습니다.
![로딩최적화](/images/loading.png)

## 1 . 로딩최적화
  로딩은 두 가지 관점으로 나눌 수 있습니다.  
  
  • 브라우저 기준(DOMContentLoaded) : 서버에서 response로 전달주는 resource들을 클라이언트가 다 응답받아 HTML과 CSS를 파싱하고 어태치하는 과정. 

  • 사용자 기준 : 사용자에게 의미있는 content를 로드하는 과정. 

### 1.1 브라우저 기준 로딩최적화
 &nbsp;브라우저는 서버로부터 resource를 전달받아 HTML과 CSS를 파싱하면서 레이아웃 구성 및 paint를 진행합니다.      
 파싱을 진행하다가 `<script>`태그와 만나게 되면 javascript를 파싱하고 즉시 실행하게 됩니다.  javascript가 실행된 이후로 그 다음 구문을 동기적으로 파싱할 수 있습니다.   
 브라우저가 효율적으로 빠르게 뷰(view)를 그리기 위해서는 HTML과 CSS를 파싱하면서 자바스크립트로 인해 block resource가 발생하는 것을 방지해야합니다.  
 즉, HTML을 읽어나가다가 script를 만나 view를 그리는 시간이 늦어지지않도록 javascript는 view가 다 그려진 시점에 파싱해야합니다.   
 html5 가 나오기 이전에는, `<script>` 태그를 `<body>` 태그가 끝나기 바로 전에 위치하게 했습니다.  
 html5에서는 외부 js resource를 받아오는 경우 defer속성이나 async 속성을 추가하여 같은 효과를 낼 수 있습니다.
  
 *단, 외부의 resource를 가져오는 script태그인 경우에만 사용가능합니다.  

 ** 엄연히 이야기하자면 defer와 async는 다른 속성이다.  
 &nbsp;&nbsp;&nbsp;defer의 경우는 외부의 source를 비동기적으로 가져온 후 html파싱이 끝난 후 파싱하게 하고,  
 &nbsp;&nbsp;&nbsp;async는 비동기적으로 외부 source를 받아온 후 그 즉시 파싱한 후 실행합니다.
 
### 1.2  사용자 기준 최적화 

 &nbsp;상위의 브라우저 기준으로 최적화를 하면 view를 빨리 그릴 수는 있으나, 엔드유저에겐 빨리 view를 그리는 것보다 가치있는 content를 보여주는 것이 중요합니다.  
 이를 FMP(First Meaningful Paint)라고 합니다.  
 SPA방식으로 많은 사이트들이 운용되고 있는데, SPA방식으로 운용하면 초기렌더링시에 resource를 전부 받아온 후 FMP가 그려지기 때문에 유저에게 이 시간을 단축시켜주어야합니다.   
 Client Side Rendering방식일 경우, 초기 렌더링 시에 webpack에서 초기 static한 index.html을 미리 내려주는 prerender-loader라는 플러그인이 존재합니다.  

## 2. 렌더링 최적화 
모든 필요한 resource들을 받고 나서, dom 요소들이 다 그려지고, 엔드유저가 원하는 액션을 취할 수 있게 되기까지를 렌더링이라고 합니다. 

### 2.1 레이아웃 스레싱

 &nbsp;dom의 레이아웃은 요소의 위치, 넓이 등의 기하학적 속성으로 이루어집니다.  
 dom 요소의 레이아웃이 자주 변경되는 경우에 dom 요소의 위치 등의 스타일 속성을 자주 바꾸는 경우에는 요소의 속성을 확인하고, 계산하고, 변경하여 dom 에 반영하는 CPU이용률이 높아집니다.  
 많은 요소들의 레이아웃이 변경되면서 변경된 속성으로 인해 트리거되어 재계산되고 재배치되어 CPU사용률이 과하게 높아지게 되면 성능을 낮춥니다.  
 javascript로 강제적으로 동기적으로 layout 후 style이 변경되도록 코드를 수정하여 CPU사용률을 낮출 수 있습니다.  
 js로 style속성을 미리 캐싱하여 불필요한 요소의 속성 계산을 방지한다면, 성능 향상에 도움이 됩니다.  
 강제 동기 레이아웃 - dom property를 읽기만 해도 발생(DOM, CSSOM, Layout)  
- 참고[https://developers.google.com/web/fundamentals/performance/rendering/avoid-large-complex-layouts-and-layout-thrashing?hl=ko]([https://developers.google.com/web/fundamentals/performance/rendering/avoid-large-complex-layouts-and-layout-thrashing?hl=ko])

### 2.2. 가상돔
 &nbsp;클라이언트 프레임워크 (React, Vue.js, Angular.js 등)은 실제의 돔과 같은 트리구조의 가상돔을 내부적으로 만듭니다.  
 가상돔에서 변경이 생기면, 실제 돔을 다 변경하지 않고,  변경점이 발생한 가상돔의 노드에 일치하는 실제 노드에 변경사항을 반영합니다.   
 이는 돔을 쉽게 조작하고, 실제 돔을 변경하면서의 불필요한 렌더링을 최소화시킵니다. 

### 2.3  웹 워커 
&nbsp;무거운 연산 작업 시 웹워커를 도입하여 스레드를 나눠서 렌더링을 동시에 진행할 수 있습니다.  
자바스크립트는 싱글스레드이지만, 브라우저에서 멀티 쓰레드를 사용할 수 있도록 웹워커 (html5)를 지원합니다.  
각 브라우저 엔진에 따라 쓰레드의 개수가 다르지만, 크롬은 5개, 파이어폭스는 4개로 알려져 있습니다.  
브라우저 버전별로 웹워커를 사용 유무는 다르기 때문에 웹워커를 통해 분산하여 연산 및 비동기처리를 하기 위해서는 브라우저별 처리가 필요합니다.  
internet explorer는 10 이상 지원합니다. webpack을 쓰는 프로젝트의 경우는 worker-loader(https://www.npmjs.com/package/worker-loader)플러그인을 사용할 수 있습니다.   

![크롬/파이어폭스 웹워커](/images/loading.png)





