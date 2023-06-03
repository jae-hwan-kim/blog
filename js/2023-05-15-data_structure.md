---
title: "JS (11)"
categories:
    - js
tags:
    - javascript

last_modified_at: 2023-05-15T15:06:58
---

# 자료구조

## ❒ 배열

### ▪︎ 선언 방식

```js
let arr = new Array();
let arr = [];
```

### ▪︎ 배열 요소의 자료형

제약이 없다.

```js
// 요소에 여러 가지 자료형이 섞여 있다.
let arr = [
    "사과",
    { name: "이보라" },
    true,
    function () {
        alert("안녕하세요.");
    },
];

// 인덱스가 1인 요소(객체)의 name 프로퍼티를 출력.
alert(arr[1].name); // 이보라

// 인덱스가 3인 요소(함수)를 실행.
arr[3](); // 안녕하세요.
```

### ▪︎ 3가지 종류의 반복문 `for`, `for .. of`, `for .. in`

-   for

```js
let arr = ["사과", "오렌지", "배"];

for (let i = 0; i < arr.length; i++) {
    alert(arr[i]);
}
```

-   for .. of

```js
let fruits = ["사과", "오렌지", "자두"];

// 배열 요소를 대상으로 반복 작업을 수행
for (let fruit of fruits) {
    alert(fruit);
}
```

-   for .. in

```js
let arr = ["사과", "오렌지", "배"];

for (let key in arr) {
    alert(arr[key]); // 사과, 오렌지, 배
}
```

### ▪︎ 배열을 비우는 방법

length 를 이용하여 배열을 쉽게 비울 수 있다. 이게 가능한 이유는 length 의 길이를 직접 조절할 수 있기 때문이다.

```js
let arr = [1, 2, 3, 4, 5];

arr.length = 2; // 요소 2개만 남기고 잘라봅시다.
alert(arr); // [1, 2]

arr.length = 5; // 본래 길이로 되돌려 봅시다.
alert(arr[3]); // undefined: 삭제된 기존 요소들이 복구되지 않습니다.
```

그렇기 때문에 `arr.length = 0;` 을 사용해 아주 간단하게 배열을 비울 수 있다.

### ▪︎ 배열 메서드

#### ↘︎ 요소를 더하거나 지우기

-   push(...items) <br>
    맨 끝에 요소 추가하기
-   pop() <br>
    맨 끝 요소 추출하기

-   shift() <br>
    첫 요소 추출하기
-   unshift(...items) <br>
    맨 앞에 요소 추가하기

-   splice(pos, deleteCount, ...items) <br>
    pos부터 deleteCount개의 요소를 지우고, items 추가하기
-   slice(start, end) <br>
    start부터 end 바로 앞까지의 요소를 복사해 새로운 배열을 만듦
-   concat(...items) <br>
    배열의 모든 요소를 복사하고 items를 추가해 새로운 배열을 만든 후 이를 반환함. items가 배열이면 이 배열의 인수를 기존 배열에 더해줌

#### ↘︎ 원하는 요소 찾기

-   indexOf/lastIndexOf(item, pos) <br>
    pos부터 원하는 item을 찾음. 찾게 되면 해당 요소의 인덱스를, 아니면 -1을 반환함

-   includes(value) <br>
    배열에 value가 있으면 true를, 그렇지 않으면 false를 반환함

-   find/filter(func) <br>
    func의 반환 값을 true로 만드는 첫 번째/전체 요소를 반환함

-   findIndex는 find와 유사함. 다만 요소 대신 인덱스를 반환함

#### ↘︎ 배열 전체 순회하기

-   forEach(func) <br>
    모든 요소에 func을 호출함. 결과는 반환되지 않음

#### ↘︎ 배열 변형하기

-   map(func) <br>
    모든 요소에 func을 호출하고, 반환된 결과를 가지고 새로운 배열을 만듦

-   sort(func) <br>
    배열을 정렬하고 정렬된 배열을 반환함

-   reverse() <br>
    배열을 뒤집어 반환함

-   split/join <br>
    문자열을 배열로, 배열을 문자열로 변환함

-   reduce(func, initial) <br>
    요소를 차례로 돌면서 func을 호출함. 반환값은 다음 함수 호출에 전달함. 최종적으로 하나의 값이 도출됨

#### ↘︎ 기타

-   Array.isArray(arr) <br>
    arr이 배열인지 여부를 판단함

-   arr.some(fn)과 arr.every(fn) <br>
    배열을 확인함. 두 메서드는 map과 유사하게 모든 요소를 대상으로 함수를 호출한다. some은 함수의 반환 값을 true로 만드는 요소가 하나라도 있는지 여부를 확인하고 every는 모든 요소가 함수의 반환 값을 true로 만드는지 여부를 확인한다. 두 메서드 모두 조건을 충족하면 true를, 그렇지 않으면 false를 반환한다.

-   arr.fill(value, start, end) <br>
    start부터 end까지 value를 채워 넣습니다.

-   arr.copyWithin(target, start, end) <br>
    start부터 end까지 요소를 복사하고, 복사한 요소를 target에 붙여넣습니다. 기존 요소가 있다면 덮어씁니다.

#### ❗️ 주의 사항

-   sort, reverse, splice는 기존 배열을 변형시킨다.

---

## ❒ 맵

맵은 키가 있는 값이 저장된 컬렉션이다.

### ▪︎ 주요 메서드와 프로퍼티

-   new Map([iterable]) <br>
    맵을 만듭니다. [key,value]쌍이 있는 iterable(예: 배열)을 선택적으로 넘길 수 있는데, 이때 넘긴 이터러블 객체는 맵 초기화에 사용된다.
    <img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/aa496c8c-9c6a-4f14-bfdd-92b3a6ac2a3c" width="90%">

-   map.set(key, value) <br>
    키를 이용해 값을 저장

-   map.get(key) <br>
    키에 해당하는 값을 반환합니다. key가 존재하지 않으면 undefined를 반환

-   map.has(key) <br>
    키가 있으면 true, 없으면 false를 반환합니다.

-   map.delete(key) <br>
    키에 해당하는 값을 삭제합니다.

-   map.clear() <br>
    맵 안의 모든 요소를 제거합니다.

-   map.size <br>
    요소의 개수를 반환합니다.

---

## ❒ 셋

셋은 중복이 없는 값을 저장할 때 쓰이는 컬렉션이다.

### ▪︎ 주요 메서드와 프로퍼티

-   new Set([iterable]) <br>
    셋을 만든다. iterable 객체를 선택적으로 전달받을 수 있는데(대개 배열을 전달받음), 이터러블 객체 안의 요소는 셋을 초기화하는데 쓰인다.

-   set.add(value) <br>
    값을 추가하고 셋 자신을 반환한다. 셋 내에 이미 value가 있는 경우 아무런 작업을 하지 않는다.

-   set.delete(value) <br>
    값을 제거한다. 호출 시점에 셋 내에 값이 있어서 제거에 성공하면 true, 아니면 false를 반환한다.

-   set.has(value) <br>
    셋 내에 값이 존재하면 true, 아니면 false를 반환한다.

-   set.clear() <br>
    셋을 비운다.

-   set.size <br>
    셋에 몇 개의 값이 있는지 센다.

---

## ❒ 위크맵 (weak map) 과 위크셋 (weak set)

자바스크립트 엔진은 가비지 컬렉션을 통해 사용 가능성이 있는 값은 메모리에 유지하고, 그렇지 않으면 삭제한다.

Map 에 어떤 데이터를 넣고, 해당 데이터를 `null` 로 할 경우, 가비지 컬렉션이 어떻게 판단할까?

Map 에 들어간 데이터에 접근할 경우 값이 유지된다. (그냥 데이터에 접근하면 null 이다.)

배열을 예시로 보자.

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/522ce7aa-1cab-478e-a42e-1b0aa280f9b0"  width="90%">

<br>

---

그렇다면 삭제하기 위해 어떻게 해야할까? 가비지 컬렉터에의해 삭제하기 위해서는 위크맵을 사용하면 된다.

예시

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/0f737714-b767-4481-82d9-f2c4108996da" width="90%">

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/a862f45f-c072-45b7-a5b2-dce566b58963" width="90%">

### ▪︎ 주요 메서드와 프로퍼티

-   weakMap.get(key)

-   weakMap.set(key, value)

-   weakMap.delete(key)

-   weakMap.has(key)

메스드가 매우 적다. 가비지 컬렉션이 일어나는 시점은 자바스크립트 엔진이 결정한다. 객체는 모든 참조를 잃었을 때, 그 즉시 메모리에서 삭제될 수도 있고, 다른 삭제 작업이 있을 때까지 대기하다가 함께 삭제될 수도 있다. 현재 위크맵에 요소가 몇 개 있는지 정확히 파악하는 것 자체가 불가능하다. 가비지 컬렉터가 한 번에 메모리를 청소할 수도 있고, 부분 부분 메모리를 청소할 수도 있다. 그래서 위크맵의 요소(키/값) 전체를 대상으로 무언가를 하는 메서드는 동작 자체가 불가능하다.

### ▪︎ 위크맵과 위크셋은 어디서 사용하는가?

#### ↘︎ 추가와 캐싱데이터

이 부분은 아직 잘 이해하지 못했다.
https://ko.javascript.info/weakmap-weakset
