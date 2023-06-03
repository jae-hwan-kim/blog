---
title: "JS (12)"
categories:
    - js
tags:
    - javascript

last_modified_at: 2023-05-15T15:06:58
---

# 구조 분해 할당

⭐️ [구조 분해할당](https://ko.javascript.info/destructuring-assignment)

<br>

## ↘︎ 구조 분해 할당?

구조 분해 할당을 사용하면 객체나 배열을 변수로 연결할 수 있다.

### ☝🏻 객체 분해하기

```js
let {prop : varName = default, ...rest} = object
```

object의 프로퍼티 prop의 값은 변수 varName에 할당되는데, object에 prop이 없으면 default가 varName에 할당된다.

연결할 변수가 없는 나머지 프로퍼티들은 객체 rest에 복사된다.

### ☝🏻 배열 분해하기

```js
let [item1 = default, item2, ...rest] = array
```

array의 첫 번째 요소는 item1에, 두 번째 요소는 변수 item2에 할당되고, 이어지는 나머지 요소들은 배열 rest 저장된다.

할당 연산자 좌측의 패턴과 우측의 구조가 같으면 중첩 배열이나 객체가 있는 복잡한 구조에서도 원하는 데이터를 뽑아낼 수 있다.
