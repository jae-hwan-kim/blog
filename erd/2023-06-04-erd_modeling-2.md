---
title: "ERD Modeling (2)"
categories:
    - ERD (Entity Relationship Diagram)
tags:
    - erd
    - backend
    - database
    - logical data modeling

last_modified_at: 2023-06-04T16:15:10
---

## 3. 논리적 데이터 모델링

데이터를 표로 전환

## 3-1. Mapping Rule

개념적 모델링에서 사용했던 ER 다이어그램을 통해 표현한 내용을 관계형 데이터베이스에 맞게 전환할 때 사용할 수 있는 방법론이다.

ER 다이어그램을 각각 다음으로 변환하면 된다.

* Entity -> Table
* Attribute -> Column
* Relation -> PK, FK

<br>

### ↘︎ 툴을 활용하여 ER 다이어그램을 테이블로 바꾸기

영상에서는 ER Master 라는 툴을 사용하지만, 우리는 ERD Cloud 를 대신 사용할 것이다.

1. Entity -> Table & Attribute -> Column

    이름, PK, 자료형, 길이, NOT NULL 등을 설정한다.
    <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/b449047f-4865-455c-abfa-f84f6e18cddf" width="80%">

<br>

2. Relation -> PK, FK

    * 1 대 1 Relation 추가!!

        1 대 1 관계에서는 PK 와 FK 설정이 헷갈린다.

        `의존성`을 따져보자. 의존성이 있는 테이블을 FK 로 설정하자. 강의에서 휴면 기능을 추가해서 PK 와 FK 설정 예시를 보였다.

        휴면 id는 저자가 없으면 존재할 수 없기 때문에 의존성이 있다. 그렇기 때문에 휴먼 id는 FK, 저자 id 를 PK 로 설정한다.

        <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/ea4a5b09-ded5-4b2b-a25b-b86a7b3c3a29" width="80%">

        Optional 추가

        <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/cc8639f4-86f4-4d18-b5b4-467b3b9eb4d9" width="80%">

    <br>

    * 1 대 N Relation 도 추가!!

        <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/048ede66-fa2b-4ce2-8f2c-fcdf0c9e1225" width="80%">

    <br>

    * N 대 M Relation 도 추가!!

        N : M 관계는 조금 까다롭다. 저자와 글의 관계 처리를 통해 배워보자.

        까다로운 이유는 다음을 보면 알 수 있다.

        * topic 테이블에 author 를 연결해보자.
            
            여러명의 저자가 들어간다.

        * author 테이블에 topic 테이블을 연결해보자.
            
            마찬가지로 여러개의 topic이 들어간다.

            <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/bf3ab82c-836b-45a0-9020-ac2466a60ee0" width="80%">
            
            ❗️ 굉장히 애매한 상황이 되는 것이다
        
            <br>

            ☝🏻 이때 필요한 것이 `Mapping Table` 이다.

            <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/c13c04ad-b821-4a80-b142-86212884bb9b" width="80%">

            <br>

            이제 `Mapping Table`을 테이블로 옮겨보자.

            <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/a2cf526b-5804-48a4-ba9a-b57dda639e6c" width="80%">


<br>

---

## 4. 물리적 데이터 모델링

데이터 베이스 툴을 이용하여 표를 구현


<br>

---

# 정리

객체를 찾는게 가장 중요한 것 같다.



<br>

---

# 참고 사이트

* 유튜브 [관계형 데이터 모델링](https://www.youtube.com/watch?v=1d38YZKCM88&list=PLuHgQVnccGMDF6rHsY9qMuJMd295Yk4sa) 을 정리한 내용입니다.



