---
layout: post
title: 오류와 에러, 예외처리란
categories: [basic]
---
 
 1. 예외처리의 관점
 
  ```
  
   예외(Exception)에 대한 대응을 할 수 있다면 예외이고, 예외처리로는 대응할 수 없는 게 에러(Error)다. 
   
   예외처리를 하더라도 어플리케이션이 생각하는 대로 handle되지 않는다면 Error고, try, catch(finally) 등으로 상황에 대해서 
   
   처리하고 handle할 수 있다면 Exception이라 할 수 있다. 
    
   
  ```   
  
 2. Runtime
 
 ```
   런타임동안 handle할 수 있다면 Exception,
   
   런타임동안 handle할 수 없다면 Error다. 
   
   런타임동안 처리할 수 있다는 의미는 Exception은 이를 의도하는 대로 handle할 수 있는 기회가 있다는 뜻이다.  

 ``` 
 
  개발자는 Error에 대해서 어떤 것도 하지 못하며, 예상할 수도 이에 대해 다루지(handle)할 수도 없다.
  
  그러나 처리할 수 있고 의도하는 대로 handle할 수 있는 Exception은 시니컬하게는 개발자가 커버해야하는 개발자의 능력(?)이다. 
  
  