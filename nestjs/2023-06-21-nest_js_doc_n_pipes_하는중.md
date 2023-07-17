---
title: "[DOCS] socketIO 공식문서 (14)"
categories:
    - socket
tags:
    - socketIO

last_modified_at: 2023-06-20T13:53:00
---

[Validation](https://docs.nestjs.com/techniques/validation) 페이지 해석

# 1. Validation

웹 애플리케이션으로 전송되는 모든 데이터의 정확성을 검증하는 것이 가장 좋습니다. 들어오는 요청의 유효성을 자동으로 검사하기 위해 Nest는 바로 사용할 수 있는 여러 파이프를 제공합니다.

-   `ValidationPipe`

-   `ParseIntPipe`
-   `ParseBoolPipe`
-   `ParseArrayPipe`
-   `ParseUUIDPipe`

유효성 검사 파이프는 강력한 [class-validator](https://github.com/typestack/class-validator) 검사기 패키지와 선언적인 유효성 검사 데코레이터를 사용합니다. `ValidationPipe`는 들어오는 모든 클라이언트 `payload`에 대해 유효성 검사 규칙을 적용하는 편리한 접근 방식을 제공하며, 특정 규칙은 각 모듈의 로컬 `class/DTO` 선언에 간단한 주석으로 선언됩니다.

<br>

---

## 1-1. 개요

[Pipes](https://docs.nestjs.com/pipes) 챕터에서는 간단한 파이프를 빌드하고 컨트롤러, 메서드 또는 전역으로 앱에 바인딩하는 과정을 통해 프로세스가 어떻게 작동하는지 보여드렸습니다. 이 장의 주제를 가장 잘 이해하려면 해당 장을 반드시 복습하세요. 여기서는 `ValidationPipe`의 다양한 실제 사용 사례에 초점을 맞추고 더욱 발전한 커스텀 기능 중 일부를 사용하는 방법을 보여드리겠습니다.

<br>

## 1-2. Using the built-in ValidationPipe

사용을 시작하려면 먼저 필요한 종속성을 설치합니다.

```sh
$ npm i --save class-validator class-transformer
```

☝🏻 `ValidationPipe`는 `@nestjs/common` 패키지에서 내보냅니다.

이 파이프는 `class-validator` 및 `class-transformer` 라이브러리를 사용하므로 사용할 수 있는 옵션이 많습니다. 파이프에 전달된 구성 개체를 통해 이러한 설정을 구성합니다.

다음은 기본 제공 옵션입니다.

```ts
export interface ValidationPipeOptions extends ValidatorOptions {
    transform?: boolean;
    disableErrorMessages?: boolean;
    exceptionFactory?: (errors: ValidationError[]) => any;
}
```

이 외에도 모든 `class-validator` 옵션(`ValidatorOptions` 인터페이스에서 상속됨)을 사용할 수 있습니다.