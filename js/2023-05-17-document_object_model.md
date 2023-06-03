---
title: "JS (13)"
categories:
    - js
tags:
    - javascript

last_modified_at: 2023-05-15T15:06:58
---

# DOM

⭐️ [DOM](https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/Introduction)

<br>

---

## ↘︎ 문서 객체 모델 ( DOM )?

자바스크립트를 이용하여 웹 문서에 접근하고 제어할 수 있도록 객체를 사용해 웹 문서를 체계적으로 정리하는 방법이다.
HTML 언어로 작성한 웹 문서의 DOM 을 HTML DOM 이라고 한다. DOM 은 웹 문서와 웹 문서를 이루는 텍스트나 이미지, 표 등 모든 요소도 각각 객체로 정의한다.

<br>

---

## ↘︎ DOM 트리

DOM 은 웹 문서의 요소를 부모와 자식으로 구분한다.

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8" />
        <title>DOM Tree</title>
    </head>
    <body>
        <h1>Do it!</h1>
        <img src="images/doit.jpg" alt="공부하는 이미지" />
    </body>
</html>
```

아래는 위 코드 요소의 부모 자식 관계를 정리했다. 이때 트리에서 가지가 갈라져 나간 항목을 노드 (node) 라고 하며, 시작부분을 루트 (root) 노드라고 한다.

<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/2e80621a-e0b2-432f-8c0e-45a920280e58"  width="90%">

조금 더 디테일하게 들어가보자. DOM 을 구성하는 기본 원칙은 다음과 같다.

```text
1. 모든 HTML 태그는 요소(element) 노드
2. HTML 태그에서 사용하느 텍스트 내용은 자식 노드인 텍스트(text) 노드
3. HTML 태그에 있는 속성은 자식 노드인 속성(attribute) 노드
4. 주석은 주석(comment) 노드
```

기본 원칙에 따라 구성하면 다음과 같다.
<img src="https://github.com/JaeHwan-s-WebServeClass/webserver-nginx/assets/85930183/3da38bd2-0ef3-47e2-b03d-156feb8007c1" width="90%">

<br>

---

## ETC

자바스크립트에 있는 객체

• 브라우저 관련 객체: 웹 브라우저에서 사용하는 정보도 객체로 나타낼 수 있습니다. 사용하는 브라우저 정보를 담고 있는 navigator 객체를 비롯해 history, location, screen 객체 등이 있습니다.

• 내장 객체: 웹 프로그래밍을 할 때 자주 사용하는 요소는 자바스크립트 안에 미리 객체로 정의되어 있는데, 이를 내장 객체라고 합니다. 예를 들어 날짜, 시간과 관련된 프로그램을 개발하려 면 Date 객체를 가져와 쉽게 사용할 수 있습니다.
