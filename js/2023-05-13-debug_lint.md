---
title: "JS (9)"
categories:
    - js
tags:
    - javascript

last_modified_at: 2023-05-15T15:06:58
---

# Chrome 으로 디버깅하기 & Linter

## Chrome 으로 디버깅하기

참고 : https://ko.javascript.info/debugging-chrome

## Linter

Linter라는 도구를 사용하면 내가 작성한 코드가 스타일 가이드를 준수하고 있는지를 자동으로 확인할 수 있다.

자동으로 스타일을 체크받다 보면, 변수나 함수 이름에 난 오타 등이 유발하는 버그를 미리 발견할 수 있어서 좋다.

### 유명 linter:

-   JSLint – 역사가 오래된 linter
    https://www.jslint.com/ <br>
-   JSHint – JSLint보다 세팅이 좀 더 유연한 linter <br>
    https://jshint.com/
-   ESLint – 가장 최근에 나온 linter <br>
    https://eslint.org/

대부분의 linter는 플러그인 형태로 유명 에디터와 통합해 사용할 수 있습니다. 원하는 스타일을 설정하는 것 역시 가능합다.

### 사용법

ESLint를 사용한다고 가정했을 때 아래 절차를 따르면 에디터와 linter를 통합해 사용할 수 있다.

1. Node.js를 설치한다.

2. npm(자바스크립트 패키지 매니저)을 사용해 다음 명령어로 ESLint를 설치한다. `npm install -g eslint`

3. 현재 작성 중인 자바스크립트 프로젝트의 루트 폴더(프로젝트 관련 파일이 담긴 폴더)에 .eslintrc라는 설정 파일을 생성한다.

4. 에디터에 ESLint 플러그인을 설치하거나 활성화한다.

### `.eslintrc 예시`

```
{
  "extends": "eslint:recommended",
  "env": {
    "browser": true,
    "node": true,
    "es6": true
  },
  "rules": {
    "no-console": 0,
    "indent": ["warning", 2]
  }
}
```

더 많은 옵션과 사용방법은 다음을 참고하자.
https://eslint.org/docs/latest/use/getting-started
