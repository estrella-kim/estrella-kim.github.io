---
layout: post
title: HTTP header의 content-disposition 설정
categories: server
---
일반적인 HTTP 응답에서 Content-disposition 응답헤더의 defualt 설정은 inline이다.

attachment 일 경우에는 컨텐츠가 로컬에서 안전하게 download할 수 있다.

filname 파라미터에 로컬에 저장되는 파일 네이밍을 정할 수 있다.

```
[main body 의 응답헤더에서]

Content-Disposition: inline
Content-Disposition: attachment
Content-Disposition: attachment; filename="filename.jpg"

```


참고 : (https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition)[https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition]