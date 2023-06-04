---
title: "ERD Modeling (4)"
categories:
    - ERD (Entity Relationship Diagram)
tags:
    - erd
    - backend
    - database
    - normaliztion

last_modified_at: 2023-06-04T23:43:10
---

## 4. 물리적 데이터 모델링

성능이 중요하다. find slow query 를 통해 최적화를 할 수 있다.(?) 최적화 방법은 3가지가 있고, 역정규화(denormalization)은 가장 나중에 고려하자.

* index
* cache
* denormalization

<br>

---

## 4-1. 역정규화 (denormalization)

정규화된 표를 성능을 위해 조작하는 것을 역정규화라고 한다. [역정규화 예제](https://docs.google.com/spreadsheets/d/1xlf6acYUziX9KgK9gOfLhdHtVWxSzIviVvIyhdwYeII/edit#gid=2096807931)를 보자.

### 컬럼 조작하기

* JOIN을 줄이기
* 파생 컬럼의 형성 : 계산작업 줄이기
* 컬럼을 기준으로 테이블 분리

<br>

### 행 조작하기

* 행을 기준으로 테이블 분리

<br>

### 관계 조작하기



<br>

---

# 참고 사이트

* 유튜브 [관계형 데이터 모델링](https://www.youtube.com/watch?v=1d38YZKCM88&list=PLuHgQVnccGMDF6rHsY9qMuJMd295Yk4sa) 을 정리한 내용입니다.



