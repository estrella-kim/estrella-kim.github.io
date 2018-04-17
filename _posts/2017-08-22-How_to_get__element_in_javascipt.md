---
layout: post
title: element를 가져올 때 
categories: [frontend]
---

```js

var tab = function(){ 

        var test= document.getElementById('test');

        var tabWrapper = document.querySelector('.module_tab ul');

        var tabList = tabWrapper.getElementsByTagName("li");
        
        var tabBtn = tabWrapper.getElementsByTagName('button');

        var tabBlock = tabWrapper.querySelectorAll('.module_tab__contents');

        console.log(test);      //<div id = "test"></div>

        console.log(tabWrapper); //<ul> ...</ul>

        console.log(tabList); //HTMLCollection(4)  length: 4    0: li.test1.test2.on 1: li2: li3: li.last __proto__: HTMLCollection

        console.log(tabBlock); //NodeList(4) length: 4 0: div.module_tab__contents 1: div.module_tab__contents 2: div.module_tab__contents 3: div.module_tab__contents __proto__: NodeList
        
}       

```

getElementById와 querySelector로 가져올 때는 DOM 구조로 가지고 오고, 

getElementsByTagName으로 가져올 때는 HTMLCollection으로 가져온다.

querySelectorAll로 가져올 때는 NodeList로 가져온다.











