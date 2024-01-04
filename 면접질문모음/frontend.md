# 프론트엔드 질문 모음

* [주로 참고한 사이트](https://velog.io/@wkahd01/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%EB%A9%B4%EC%A0%91-%EB%AC%B8%EC%A0%9C-%EC%9D%80%ED%96%89-HTML-%EC%A7%88%EB%AC%B8-%EB%8B%B5%EB%B3%80)

## 중요도 5

### Q 홈페이지가 사용자에게 보이는 순서 (브라우저 렌더링 과정)

1. 주소창에 입력된 주소를 통해 서버를 찾아감
2. 이후 DNS 가 연결해줄 곳을 찾음 (실제 서버)
3. 서버에서 HTML 파일을 클라이언트로 전송
4. HTML 문서는 파싱되어 DOM 을 생성 (객체 형식)
5. 중간에 CSS를 로드하는 link 혹은 style 태그를 만나면 DOM 생성을 중지
6. CSS를 파싱하고 CSSOM을 생성
7. 만들어진 DOM과 CSSOM은 렌더링을 위해 렌더 트리로 결합
8. script 태그를 만나면, CSS와 동일하겨 JS코드를 실행하기 위해 파싱을 중단
9. JS 엔진을 실행하고 JS 코드를 파싱

<br>

⭐️ 자바스크립트가 DOM, CSSOM을 변경하는 경우 리렌더링을 한다.

    리플로우 : 레이아웃 계산을 다시 하는 것
    리페인트 : 재결합된 렌더 트리를 기반으로 다시 페인트를 하는 것

⭐️ script 태그를 만날 때마다 파싱이 중단되는 문제를 script 태그 뒤에 async 혹은 defer 를 붙여줌으로써 해결할 수 있다.

    aysnc : HTML 파싱, JS 파일 로드가 동시에 진행
    defer : DOM 생성이 완료된 직후, JS의 파싱과 실행이 진행


<br>

🤔 궁금한 것 <br>
* DNS 가 연결해줄 곳을 찾는다는게 무슨 말이야?
* 렌더 트리가 뭐야?
* [리플로우 & 리페인트?](https://mong-blog.tistory.com/entry/%EB%A6%AC%ED%94%8C%EB%A1%9C%EC%9A%B0-%EB%A6%AC%ED%8E%98%EC%9D%B8%ED%8A%B8%EC%99%80-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EB%A0%8C%EB%8D%94%EB%A7%81-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)

<br>

---

### Q 호이스팅이란? -> var, let, const, 함수선언식, 함수표현식

[참고 사이트](https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html)

모든 선언이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징.

자바스크립트 함수는 실행되기 전에 함수 안에 필요한 변수값들을 모두 모아서 유효 범위의 최상단에 선언한다. 자바스크립트 Parser가 함수 실행 전 해당 함수를 한 번 훑는다. 함수 안에 존재하는 변수/함수선언에 대한 정보를 기억하고 있다가 실행시킨다.

var 변수 선언과 함수선언문에서만 호이스팅이 일어난다.
* var 변수/함수의 선언만 위로 끌어 올려지며, 할당은 끌어 올려지지 않는다.
* let/const 변수 선언과 함수표현식에서는 호이스팅이 발생하지 않는다.

예시 )

```js
console.log(name1) // undefined 출력
var name1 = '자몽';

///////////////////

console.log(name2) // ReferenceError 에러출력
let name2 = '자몽';
```




<br>

---

### Q 클로저란? -> ❗️여기부터 다시봐야함

C 의 포인터처럼 중요한 개념이다.

[참고 사이트](https://unikys.tistory.com/309)

<br>

---

### Q CSS에서 margin과 padding 이란?

* margin 은 바깥쪽 여백
* padding 은 안쪽 여백

<br>

---

### Q CSS에서 Position 이란?

<br>

---

### Q REST API 란?

<br>

---

# 참고 사이트

* [1](https://velog.io/@wkahd01/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%EB%A9%B4%EC%A0%91-%EB%AC%B8%EC%A0%9C-%EC%9D%80%ED%96%89-HTML-%EC%A7%88%EB%AC%B8-%EB%8B%B5%EB%B3%80)
* [2](https://h5bp.org/Front-end-Developer-Interview-Questions/translations/korean/)
* [3](https://realmojo.tistory.com/300)