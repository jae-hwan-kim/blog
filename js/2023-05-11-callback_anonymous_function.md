---
title: "JS (7)"
categories:
    - js
tags:
    - javascript

last_modified_at: 2023-05-15T15:06:58
---

# ⭐️ 콜백 함수와 익명 함수

## 콜백 함수

함수를 값처럼 전달하는 경우를 보자.(또 다른 함수 표현식을 보자는 이야기) 다음과 같은 예시가 있다.

ask 함수는 question 과 yes, no 라는 매개변수를 갖고 있다.

-   질문에 대한 함수
-   Yes 라고 대답한 경우 실행하는 함수
-   No 라고 대답한 경우 실행하는 함수

ask 함수 외에 `showOk()` 와 `showCancel()` 함수를 만들었다.

이제 ask 함수를 다음과 같이 호출한다.

`ask("동의하십니까?", showOk, showCancel);`

```js
function ask(question, yes, no) {
    if (confirm(question)) yes();
    else no();
}

function showOk() {
    alert("동의하셨습니다.");
}

function showCancel() {
    alert("취소 버튼을 누르셨습니다.");
}

// 사용법: 함수 showOk와 showCancel가 ask 함수의 인수로 전달됨
ask("동의하십니까?", showOk, showCancel);
```

ask 함수의 구조에 따라, question 을 실행하고 참인 경우 yes 함수를 거짓인 경우 no 함수를 호출한다.

⭐️ 실무에서 이러한 방법이 아주 유용하게 쓰인다. 여기서 함수 ask의 인수, `showOk`와 `showCancel` 를 **`콜백 함수`** 또는 **`콜백`** 이라고 부른다.

<br>

---

## 익명 함수

ask(...) 안에 함수를 선언했다. 이렇게 이름 없이 선언한 함수를 `익명 함수(anonymous function)` 라고 부른다.

익명 함수는 (변수에 할당된 게 아니기 때문에) ask 바깥에선 접근할 수 없다. 위 예시는 의도를 가지고 이렇게 구현하였기 때문에 바깥에서 접근할 수 없어도 문제가 없다!

```js
function ask(question, yes, no) {
    if (confirm(question)) yes();
    else no();
}

ask(
    "동의하십니까?",
    function () {
        alert("동의하셨습니다.");
    },
    function () {
        alert("취소 버튼을 누르셨습니다.");
    },
);
```
