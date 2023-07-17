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

옵션 생략

<br>

---

## Auto-validation

애플리케이션 수준에서 `ValidationPipe` 를 바인딩하여 모든 엔드포인트가 잘못된 데이터를 수신하지 않도록 보호하는 것부터 시작하겠습니다.

```ts
async function bootstrap() {
    const app = await NestFactory.create(AppModule);
    app.useGlobalPipes(new ValidationPipe());
    await app.listen(3000);
}
bootstrap();
```

파이프를 테스트하기 위해 기본 엔드포인트를 만들어 보겠습니다.

```ts
@Post()
create(@Body() createUserDto: CreateUserDto) {
  return 'This action adds a new user';
}
```

💡 HINT - TypeScript는 `generics` 이나 `interfaces` 에 대한 메타데이터를 저장하지 않으므로 DTO에서 제네릭이나 인터페이스를 사용할 경우 `ValidationPipe`가 들어오는 데이터의 유효성을 제대로 검사하지 못할 수 있습니다. 따라서 DTO에 구체적인 클래스를 사용하는 것이 좋습니다.

이제 `CreateUserDto` 에 몇 가지 유효성 검사 규칙을 추가할 수 있습니다. [여기](https://github.com/typestack/class-validator#validation-decorators)에 자세히 설명된 `class-validator` 검사기 패키지에서 제공하는 데코레이터를 사용하여 이 작업을 수행합니다. 이렇게 하면 CreateUserDto를 사용하는 모든 경로에 이러한 유효성 검사 규칙이 자동으로 적용됩니다.

```ts
import { IsEmail, IsNotEmpty } from "class-validator";

export class CreateUserDto {
    @IsEmail()
    email: string;

    @IsNotEmpty()
    password: string;
}
```

이러한 규칙을 적용하면 요청 본문에 잘못된 이메일 속성이 포함된 요청이 엔드포인트에 도달하면 애플리케이션이 자동으로 400 잘못된 요청 코드와 함께 다음 응답 본문으로 응답합니다:

```ts
{
  "statusCode": 400,
  "error": "Bad Request",
  "message": ["email must be an email"]
}
```

요청 본문의 유효성을 검사하는 것 외에도, 다른 요청 객체 프로퍼티에도 `ValidationPipe` 를 사용할 수 있습니다. 엔드포인트 경로에 `:id` 를 허용하고 싶다고 가정해 보겠습니다. 이 요청 매개변수에 숫자만 허용되도록 하기 위해 다음 구문을 사용할 수 있습니다:

```ts
@Get(':id')
findOne(@Param() params: FindOneParams) {
  return 'This action returns a user';
}
```

`FindOneParams` 는 DTO와 마찬가지로 클래스 유효성 검사기를 사용하여 유효성 검사 규칙을 정의하는 클래스일 뿐입니다. 다음과 같이 보일 것입니다:

```ts
import { IsNumberString } from "class-validator";

export class FindOneParams {
    @IsNumberString()
    id: number;
}
```

<br>

---

## Disable detailed errors

오류 메시지는 요청에 무엇이 잘못되었는지 설명하는 데 도움이 될 수 있습니다. 그러나 일부 프로덕션 환경에서는 자세한 오류를 비활성화하는 것을 선호합니다. 이렇게 하려면 옵션 객체를 `ValidationPipe`에 전달하면 됩니다:

```ts
app.useGlobalPipes(
    new ValidationPipe({
        disableErrorMessages: true,
    }),
);
```

따라서 응답 본문에 자세한 오류 메시지가 표시되지 않습니다.

<br>

---

## Stripping properties

또한, `ValidationPipe` 는 메서드 핸들러가 수신해서는 안 되는 프로퍼티를 필터링할 수 있습니다. 이 경우 허용 가능한 속성을 화이트리스트에 추가할 수 있으며, 화이트리스트에 포함되지 않은 속성은 결과 객체에서 자동으로 제거됩니다. 예를 들어, 처리기가 이메일 및 비밀번호 속성을 기대하지만 요청에 나이 속성도 포함된 경우 이 속성은 결과 DTO에서 자동으로 제거될 수 있습니다. 이러한 동작을 사용하려면 화이트리스트를 `true` 로 설정하세요.

true로 설정하면 화이트리스트에 없는 프로퍼티(유효성 검사 클래스에 데코레이터가 없는 프로퍼티)가 자동으로 제거됩니다.

또는 화이트리스트에 없는 속성이 있는 경우 요청 처리를 중지하고 사용자에게 오류 응답을 반환할 수 있습니다. 이 기능을 사용하려면 `whitelist`를 `true` 로 설정하는 것과 함께 `forbidNonWhitelisted` 옵션 속성을 `true` 로 설정하세요.

<br>

---

## Transform payload objects#

네트워크를 통해 들어오는 페이로드는 일반 JavaScript 객체입니다. 유효성 검사 파이프는 페이로드를 DTO 클래스에 따라 입력된 객체로 자동 변환할 수 있습니다. 자동 변환을 활성화하려면 `transform` 을 `true` 로 설정합니다. 이 작업은 메서드 수준에서 수행할 수 있습니다:

```ts
@Post()
@UsePipes(new ValidationPipe({ transform: true }))
async create(@Body() createCatDto: CreateCatDto) {
  this.catsService.create(createCatDto);
}
```

이 동작을 전역적으로 사용하려면 전역 파이프에서 옵션을 설정합니다:

```ts
app.useGlobalPipes(
    new ValidationPipe({
        transform: true,
    }),
);
```

자동 변환 옵션을 활성화하면 `ValidationPipe`는 기본 유형 변환도 수행합니다. 다음 예제에서 `findOne()` 메서드는 추출된 `id` 경로 매개변수를 나타내는 하나의 인수를 받습니다:

```ts
@Get(':id')
findOne(@Param('id') id: number) {
  console.log(typeof id === 'number'); // true
  return 'This action returns a user';
}
```

기본적으로 모든 경로 매개변수와 쿼리 매개변수는 네트워크를 통해 문자열로 전달됩니다. 위의 예제에서는 메서드 서명에서 ID 유형을 숫자로 지정했습니다. 따라서 ValidationPipe는 문자열 식별자를 숫자로 자동 변환하려고 시도합니다.