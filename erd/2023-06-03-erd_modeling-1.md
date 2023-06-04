---
title: "ERD Modeling (1)"
categories:
    - ERD (Entity Relationship Diagram)
tags:
    - erd
    - backend
    - database

last_modified_at: 2023-06-03T16:15:10
---

정보를 데이터 베이스 표에 저장하는 것.

☝🏻 관계형 데이터베이스

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/7b16557b-db34-410c-94ed-7327b63372b5" width="90%">

<br>

---
# 데이터 모델링을 위한 순서

1. 업무 파악
2. 개념적 데이터 모델링
3. 논리적 데이터 모델링
4. 물리적 데이터 모델링

<br>

---
## 1. 업무 파악

* 업무 파악을 할 때 UI 를 같이 그려보자.

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/383e7964-80a3-4f1d-8759-10f35893da43" width="90%">

<br>

---

## 2. 개념적 데이터 모델링

개념적 모델링이 중요하다. 이 모델링을 잘해놓는다면 논리적 모델링과 물리적 모델링은 기계적인 일이 될 것이다.

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/93f906ad-599d-4580-9f83-14238fff7c36" width="90%">

위 그림은 개념적 데이터 모델링을 위한 `ERD(Entity Relationship Diagram)`라고 한다. UI 를 참고하여 ERD를 그리는 것이 중요하다.

여기서 ERD 를 구성하는 3가지 구성요소를 볼 수 있다.

1. 정보
    * Attribute (속성)
    * 동그라미로 묶인 것 <br>
        * 본문, 작성일, 작성자, 이름, 소개, 저자번호 등
    * Table 이 될 것이다.

<br>

2. 정보의 그룹
    * Entity (객체)
    * 네모로 묶인 것 <br>
        * 댓글, 저자, 글
    * Column 이 될 것이다.

<br>

3. 정보의 관계
    * Relation (관계)
    * 다이아로 묶인 것 <br>
        * 속하다, 작성한다
    * PK, FK 가 될 것이다.

<br>

## 2-1. Identifier

속성에서 식별자를 뽑아야한다.

* 하나의 키로 식별하는 경우
    <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/3bf6608f-e3f1-4cea-979c-916ebb746097" width="90%">

* 두 개의 키로 식별하는 경우
    <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/9235b90f-3120-4aeb-9988-1947c05a6cc9" width="90%">

<br>

개념적 모델링 ERD 에 식별자를 추가해보자.

* 저자, 글, 댓글 Entity 의 각 Attribute 를 보면 적절한 식별자가 없기 때문에 `아이디` 를 추가하여 식별자를 만들었다.

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/fee7321d-b1b3-4282-ade9-ea4edf405d08" width="90%">


<br>

## 2-2. Relationship

관계는 PK (Primary Key) 와 FK (Foreign Key) 가 연결되면서 형성된다. 아래 그림에서 글 Entity 의 저자 아이디가 FK 이고, 저자 Entity 의 아이디가 PK 이다.

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/0f851a65-7042-43b3-95df-cc5c43a6775e" width="90%">

<br>

개념적 모델링 ERD 에 관계를 추가해보자.

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/2cb9b359-14cd-48e2-9be9-6d13ce0365d4" width="90%">

<br>

## 2-3. Cardinality

* 1:1

    <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/255e344d-7a03-4634-8963-cb10615b0f33" width="90%">

<br>

* 1:N

    <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/137f954b-c7d9-495e-9e3b-738b128270ca" width="90%">

<br>

* N:M

    실제 데이터베이스로는 구현이 어려워서, 연결 테이블이 필요하다.
    <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/b8fd013f-ba37-450a-885d-6682ba2cf6bd" width="90%">

<br>

## 2-4. Optionality

* 선택

    <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/fbdcdadc-2a35-4af2-976a-904457ecb8eb" width="90%">

* 필수

    <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/7552ec36-06c2-417d-8fcf-f44cfb7f358d" width="90%">

* Cardinality 와 함께 표현

    <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/12a73667-bde5-4624-b87c-1a2120fff674" width="90%">

<br>

개념적 모델링 ERD에 Cardinality 와 Optionality 를 추가해보자.

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/99783a4d-70d8-4aec-a885-58b2c9e25361" width="80%">

<br>

---

# 참고 사이트

* 유튜브 [관계형 데이터 모델링](https://www.youtube.com/watch?v=1d38YZKCM88&list=PLuHgQVnccGMDF6rHsY9qMuJMd295Yk4sa) 을 정리한 내용입니다.


