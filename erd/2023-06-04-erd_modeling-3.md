---
title: "ERD Modeling (3)"
categories:
    - ERD (Entity Relationship Diagram)
tags:
    - erd
    - backend
    - database
    - normaliztion

last_modified_at: 2023-06-04T16:15:10
---

## 정규화  (Normalization)

[정규화 예제](https://docs.google.com/spreadsheets/d/1zmN7qQYjKGkQW0aSKFQxEJ-yLVXYM27AHgnsybJGvFM/edit#gid=251854387)가 있다.

다음 이미지를 보면 관계형 데이터베이스로 보기에 부적절한 테이블이 있다.

* 중복된 값 (붉은색)
* 여러개의 값 (푸른색)

    <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/1eda28fd-5bef-4a90-8b1c-5c5aaff75a06" width="80%">

이 값들을 관계형 데이터에 맞게 정규화해보자.

## 제 1 정규형

제 1 정규형은 `Atomic columns` 이다. 각 행의 열의 값이 원자적이어야 한다는 규칙이다. 즉, 하나의 값을 가져야 한다는 의미이다.

`tag` 를 보면, 2개의 값이 있다. 2개의 값이 있다면 다음과 같은 sql 문에서 문제가 생긴다.

```sql
SELECT * FROM topic WHERE tag = 'free'
SELECT * FROM topic ORDER BY tag
```

이러한 문제를 해소시킨 표를 제 1 정규형을 만족시킨 표라고 한다.

tag 를 분리한 후, topic 과 tag 에 대한 `Mapping Table`을 만들었다.

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/eaa4d53f-8311-47d0-82ea-da5e73dd9a5c" width="90%">


<br>

---

## 제 2 정규형

제 2 정규형은 `No partial dependencies` 이다. 즉, 부분 종속성이 없어야 한다는 의미이다. 다시 말해, 표의 기본키 중에 중복키가 없어야 한다는 것이다.

연붉은색을 보면 중복이 있다. price를 보면 type에 따라 나뉜다. 가운데 있는 description 부터 author_profile 은 관련이 없다.

그렇기 때문에 topic 테이블을 topic_type으로 나누고, 중복을 없앴다.

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/11e5e96e-5533-486a-acdc-3e644f05f26f" width="80%">


<br>

---

## 제 3 정규형

제 3 정규형은 `No transitive dependencies` 이다. 직역하면 이행적 종속성이 없어야 한다는 의미이다.

이행적 종속성은 종속이 종속되어 있는 것을 의미한다. 아래 이미지를 보면 author_id 는 title 에 종속되고 author_name 과 author_profile 은 author_id 에 종속된다.

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/8bdb70cc-4e58-4526-8d45-c5d0703ce877" width="80%">

어떻게 해결할까?! author_id 에서 author_profile 을 분리한다. 그리고 중복을 제거한다. 다음과 같은 형태를 통해 제 3정규화를 만족시키자.

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/36bd2653-c8a7-4934-912d-c12eb8e92bec" width="80%">

<br>

---


<br>

---

# 참고 사이트

* 유튜브 [관계형 데이터 모델링](https://www.youtube.com/watch?v=1d38YZKCM88&list=PLuHgQVnccGMDF6rHsY9qMuJMd295Yk4sa) 을 정리한 내용입니다.



