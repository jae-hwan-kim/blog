---
title: "[DOCS] Nest JS 공식문서 (5)"
categories:
    - nest js
tags:
    - nest js

last_modified_at: 2023-07-07T12:22:00
---

[Security](https://docs.nestjs.com/openapi/security#oauth2-authentication) 페이지 해석

# 1. Security

특정 작업에 어떤 보안 메커니즘을 사용해야 하는지 정의하려면 @ApiSecurity() 데코레이터를 사용하세요.

```ts
@ApiSecurity("basic")
@Controller("cats")
export class CatsController {}
```

애플리케이션을 실행하기 전에 `DocumentBuilder` 를 사용하여 기본 문서에 보안 정의를 추가하는 것을 잊지 마세요:

```ts
const options = new DocumentBuilder().addSecurity("basic", {
    type: "http",
    scheme: "basic",
});
```

가장 많이 사용되는 인증 기술 중 일부는 기본으로 제공되므로(예: 기본 및 무기명) 위와 같이 보안 메커니즘을 수동으로 정의할 필요가 없습니다.

<br>

---

## Basic authentication

기본 인증을 사용하려면 `@ApiBasicAuth()`를 사용합니다.

```ts
@ApiBasicAuth()
@Controller("cats")
export class CatsController {}
```

애플리케이션을 실행하기 전에 `DocumentBuilder` 를 사용하여 기본 문서에 보안 정의를 추가하는 것을 잊지 마세요:

```ts
const options = new DocumentBuilder().addBasicAuth();
```

<br>

---

## Bearer authentication

Bearer authentication 을 활성화하려면 `@ApiBearerAuth()` 를 사용합니다.

```ts
@ApiBearerAuth()
@Controller("cats")
export class CatsController {}
```

애플리케이션을 실행하기 전에 DocumentBuilder를 사용하여 기본 문서에 보안 정의를 추가하는 것을 잊지 마세요:

```ts
const options = new DocumentBuilder().addBearerAuth();
```

<br>

---

## OAuth2 authentication

OAuth2 를 활성화하려면 `@ApiOAuth2()` 를 사용합니다.

```ts
@ApiOAuth2(["pets:write"])
@Controller("cats")
export class CatsController {}
```

애플리케이션을 실행하기 전에 DocumentBuilder를 사용하여 기본 문서에 보안 정의를 추가하는 것을 잊지 마세요:

```ts
const options = new DocumentBuilder().addOAuth2();
```

<br>

---

## Cookie authentication

쿠키 인증을 활성화하려면 `@ApiCookieAuth()`를 사용합니다.

```ts
@ApiCookieAuth()
@Controller("cats")
export class CatsController {}
```

애플리케이션을 실행하기 전에 DocumentBuilder를 사용하여 기본 문서에 보안 정의를 추가하는 것을 잊지 마세요:

```ts
const options = new DocumentBuilder().addCookieAuth('optional-session-id');
```