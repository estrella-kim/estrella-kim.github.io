---
layout: post
title: Node.js 와 express 사용하여 view page 보여주기(+ html)
categories: [server]
---
Node.js 와 Express 프레임워크로 만든 웹서비스에서 뷰페이지를 보여주도록 설정해주면서 우여곡절을 겪으면서 render 메소드와 send메소드의 차이를 알게 되었다.

```javascript
const express = require('express');
const app = express();

//생략

```
#sendFile 와 render의 차이

##render 메소드
```javascript
app.render(view, [locals], callback)
```

서버에서 rendering 된 HTML을 반환하여 응답해준다. 렌더링해주기 위해서 view engine를 설정해주어서 interpret해주어야한다.  
view 엔진 설정을 해주어야한다. 나같은 경우 html을 렌더링해주려했기 때문에 engine 설정을 아래와 같이 해주었다.

```javascript
const engine = require('ejs-locals');

app.engine('html', require('ejs').renderFile );
app.set('view engine', 'html');
app.set('views', __dirname + '/pulic');

app.get('*', function(req, res) {
    app.render('index');
})
```
그러나 만들고자 했던 서비스는 api서버의 역할을 해주고 싶었기때문에 위와 같이 server에서 html을 렌더링해주는것은 뷰를 렌더링해서 응답한다는 의미에서 적합하지 않았다.
또한 render메소드가 브라우저에게 string으로 전달만 해줄뿐 브라우저에서 결국 렌더링해주기 때문에 무의미한 일을 해주었다.
따라서 sendFile로 html 파일을 스트링으로 보내주고, 브라우저가 받은 파일을 렌더링해주는 방법이 더 적합했다.


```javascript
const template = path.join(__dirname, './public', 'index.html');

app.get('*', function(req, res) {
    app.sendFile(template);
})
```
