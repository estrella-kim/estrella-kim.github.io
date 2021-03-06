---
layout: post
title: 스키마(schema)란
categories: [server]
------
   layout: post
   title: 스키마(schema)란 : 데이터베이스에서의 스키마와 앱에서의 스키마
   categories: [server]
   ---

   ### 데이테베이스의 스키마

    컴퓨터 과학에서 데이터베이스 스키마(database schema)는 데이터베이스에서 자료의 구조, 자료의 표현 방법, 자료 간의 관계를 형식 언어로 정의한 구조이다. 데이터베이스 관리 시스템(DBMS)이 주어진 설정에 따라 데이터베이스 스키마를 생성하며, 데이터베이스 사용자가 자료를 저장, 조회, 삭제, 변경할 때 DBMS는 자신이 생성한 데이터베이스 스키마를 참조하여 명령을 수행한다.

    스키마는 3층 구조로 되어있다.

    외부 스키마(External Schema) : 프로그래머나 사용자의 입장에서 데이터베이스의 모습으로 조직의 일부분을 정의한 것
    개념 스키마(Conceptual Schema) : 모든 응용 시스템과 사용자들이 필요로하는 데이터를 통합한 조직 전체의 데이터베이스 구조를 논리적으로 정의한 것
    내부 스키마(Internal Schema) : 전체 데이터베이스의 물리적 저장 형태를 기술하는 것


  ### 앱에서의 스키마


  외부에서 자신의 앱에 접근할 수 있도록 해주는 하나의 통로 역할을 해준다.
  외부에서 앱을 실행할 때, 해당 앱에 대한 정보를 알고 있어야하는데, URL스키마를 알고 있음으로써 접근할 수 있다.
