---
title: '[Nomad] Nest JS 테스트하는 법'
categories:
  - Nest js
tags:
  - typescript
  - backend
  - framework
  - API
  - jest
  - unit test
  - e2e test
last_modified_at: 2023-05-31T16:07:58
---

Nest JS 를 이용해서 API 를 만들고, TEST 하는 방법을 배울 것이다. 먼저 `package.json` 파일의 `script` 부분을 보자.

<img src="https://github.com/jae-hwan-kim/nest_js/assets/85930183/c28ba505-0b01-42e5-acf3-f538b90f5221" width="90%">

다양한 테스트 커맨드가 있다. `npm run`과 함께 사용하며, `.spec.ts`로 끝나는 파일로 테스트한다.

<br>

### ↘︎ "test:cov":"jest --coverage"

`test:cov` 는 파일 내부의 코드들이 얼마나 테스팅 됐는지 알려준다. 만약 함수가 4개인데 1개만 테스트했다면 낮은 수치를 보여줄 것이다.

```sh
npm run test:cov
```

<img src="https://github.com/jae-hwan-kim/nest_js/assets/85930183/03242018-f2bd-46c4-9b1e-d859c529189e" width="80%">

<br>

---

### ↘︎ "test:watch":"jest --watch"

여러가지 옵션을 통해 하고 싶은 테스트를 진행할 수 있다.

☝🏻 여기서 할 수 있는 테스트의 종류에는 `유닛 테스트`와 `end to end(e2e) 테스트`가 있다. 유닛 테스트는 함수 단위로 테스트하는 것이고, ene to end(e2e)는 사용자 관점의 테스트로 사용자가 어떤 링크를 클릭하면 잘 이동하는지와 같은 것들을 테스트한다.

<br>

---

## ❒ jest

자바스크립트를 아주 쉽게 테스팅하는 npm 패키지이다. 파일을 보면 `.spec.ts` 로 끝나는 파일이 있는데 테스트를 포함하고 있는 파일이다. 사실 테스트하고 싶은 파일 뒤에 `.spec.ts`를 붙이면 된다.

아래는 `MoviesService.service.spec.ts` 파일이고, `MoviesService`를 테스트한다.

```ts
import { Test, TestingModule } from '@nestjs/testing';
import { MoviesService } from './movies.service';

describe('MoviesService', () => {
  let service: MoviesService;

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      providers: [MoviesService],
    }).compile();

    service = module.get<MoviesService>(MoviesService);
  });

  it('should be defined', () => {
    expect(service).toBeDefined();
  });
});
```

- `describe`
  - 테스트에 대해 설명하겠다는 의미이다.
- `beforeEach`
  - 테스트를 하기전에 실행된다.
- `it`

  - it 는 individual test(개별 테스트)의 줄임말로 테스트 케이스이다.

- `beforeEach` 외에도 `afterEach`, `beforeAll`, `afterAll` 등 많은 `Hook` 이 있다.

<br>

---

## ❒ 어떻게 테스트를 하는가?

```ts
it('should be 4', () => {
  expect(2 + 2).toEqual(4);
});
```

위처럼 `it` 함수를 활용하면된다. 해석하면 이렇다.

- 2 + 2 는 4 와 같다.

아래를 보면 테스트 결과를 확인할 수 있고, console 이 찍힌 모습을 확인할 수 있다.

<img src="https://github.com/jae-hwan-kim/nest_js/assets/85930183/90bb38f1-5938-448e-8297-a8e9ec1abef2" width="80%">

<br>

❗️ 틀렸을 경우 다음과 같이 출력된다.

<img src="https://github.com/jae-hwan-kim/nest_js/assets/85930183/d0e6c154-8bae-40d5-917e-4381df1922f8" width="80%">

<br>

---

## ❒ 실제 함수를 이용해서 유닛 테스트해보자

☝🏻 `npm run test:watch`를 실행하고 테스트 코드를 작성해도 되고, 모두 작성하고 실행해도 된다.

아래 파일을 보면 2개의 함수를 비교해겠다는 `describe` 가 2개 있다. 그리고 각 `describe`에 `it`가 각각 1개, 2개가 있다.

```ts
// movies.service.service.ts 의 getAll 을 테스트하는 함수
// 'getAll' 함수의 반환값이 Array 인지 테스트
describe('getAll', () => {
  it('should return an array', () => {
    const result = service.getAll();
    expect(result).toBeInstanceOf(Array);
  });
});

// movies.service.service.ts 의 getOne 을 테스트하는 함수
describe('getOne', () => {
  it('should return a movie', () => {
    service.create({
      title: 'Test Movie',
      genres: ['test'],
      year: 2000,
    });
    const movie = service.getOne(1);
    expect(movie).toBeDefined();
    // expect(movie.id).toEqual(1);
  });

  it('should throw 404 error', () => {
    try {
      service.getOne(999);
    } catch (e) {
      expect(e).toBeInstanceOf(NotFoundException);
      // expect(e.message).toEqual(`Movie with ID 999 not found.`);
    }
  });
});
```

<br>

---

쪼개서 보자.

### 1. `getAll` 함수를 테스트한다.

`expect`에 함수의 리턴값을 넣고, `toBeInstanceOf(Array)`를 통해 반환값이 `Array` 인지 확인한다.

```ts
describe('getAll', () => {
  it('should return an array', () => {
    const result = service.getAll();
    expect(result).toBeInstanceOf(Array);
  });
});
```

<br>

---

### 2. `getOne` 함수를 테스트한다.

`create`으로 새로운 요소를 만들고, `getOne(1)`로 잘만들어졌는지 확인한다.

- `toBeDefined`이란 함수로 id 가 1인 요소가 생성됬는지 테스트한다.
- `try ~ catch`를 통해 에러처리도 잘됐는지 확인한다. 이때 `toBeInstanceOf(NotFoundException)`로 에러 객체도 확인가능하다.

```ts
describe('getOne', () => {
  it('should return a movie', () => {
    service.create({
      title: 'Test Movie',
      genres: ['test'],
      year: 2000,
    });
    const movie = service.getOne(1);
    expect(movie).toBeDefined();
    // expect(movie.id).toEqual(1);
  });

  it('should throw 404 error', () => {
    try {
      service.getOne(999);
    } catch (e) {
      expect(e).toBeInstanceOf(NotFoundException);
      // expect(e.message).toEqual(`Movie with ID 999 not found.`);
    }
  });
});
```

<br>

---

실행 결과는 다음과 같다.

<img src="https://github.com/jae-hwan-kim/nest_js/assets/85930183/ec45cd5e-133a-4405-b5d5-d827f752c1f8"  width="100%">

이와 같은 방식으로 함수들을 테스트할 수 있다.

<br>

---

## ❒ 실제 함수를 이용해서 e2e 테스트해보자

e2e 테스트는 test 폴더에 있는 파일로 한다. 프로젝트 생성 초기에 함께 생성된다.

<img src="https://github.com/nomadcoders/hi-nest/assets/85930183/2cd1457a-cdbd-404f-8fb6-62b98f807d90" width="90%">

이렇게 생겼다.

```ts
import { Test, TestingModule } from '@nestjs/testing';
import { INestApplication } from '@nestjs/common';
import * as request from 'supertest';
import { AppModule } from '../src/app.module';

describe('AppController (e2e)', () => {
  let app: INestApplication;

  beforeEach(async () => {
    const moduleFixture: TestingModule = await Test.createTestingModule({
      imports: [AppModule],
    }).compile();

    app = moduleFixture.createNestApplication();
    await app.init();
  });

  it('/ (GET)', () => {
    return request(app.getHttpServer())
      .get('/')
      .expect(200)
      .expect('Hello World!');
  });
});
```

<br>

---

쪼개서 보자.

### 1. `/ (GET)` API를 테스트한다.

아래 테스트는 다음을 의미한다.

1. `/` URL 로 `Get` 메서드를 테스트한다.
2. `200` 상태 코드가 기대된다.
3. `Hello World` 가 기대된다.

즉, Controller, Service, Pipe 의 결과에 대해 모든 테스트를 하고 있다는 뜻이기도 하다.

```ts
it('/ (GET)', () => {
  return request(app.getHttpServer())
    .get('/')
    .expect(200)
    .expect('Hello World!');
});
```

<br>

---

### 실행해보자

`npm run test:e2e`를 입력하면 테스트를 시작한다. 다음은 실패할 경우이다.

<img src="https://github.com/nomadcoders/hi-nest/assets/85930183/e7bd9a1e-7c85-4d2d-bf8a-7a58ffee5aee" width="90%">

성공하면 이렇게 출력된다.

<img src="https://github.com/nomadcoders/hi-nest/assets/85930183/d86f9a35-2c76-46ec-9172-611d281f2576" width="90%">

<br>

---

### 더 많은 테스트를 해보자.

GET, POST, DELETE 테스트!

```ts
describe('/movies', () => {
  it('GET', () => {
    return request(app.getHttpServer()).get('/movies').expect(200).expect([]);
  });
  it('POST', () => {
    return request(app.getHttpServer())
      .post('/movies')
      .send({
        title: 'Test',
        year: 2000,
        genres: ['test'],
      })
      .expect(201);
  });
  it('POST 400', () => {
    return request(app.getHttpServer())
      .post('/movies')
      .send({
        title: 'Test',
        year: 2000,
        genres: ['test'],
        other: 'thing',
      })
      .expect(400);
  });
  it('DELETE', () => {
    return request(app.getHttpServer()).delete('/movies').expect(404);
  });
});
```

<br>

---

## 적절한 테스트를 위한 여러가지 TIP

### 1.

테스트 파일을 보면, 테스트를 실행할 때마다 `app` 을 새로 만든다.

```ts
...
  return request(app.getHttpServer())
...
```

`POST`에서 movie를 하나 생성하는데, `POST` 테스트가 끝나면 이 요소는 사라지게된다. 즉, 데이터베이스가 비워진다. 그래서 다른 테스트를 할 때 매번 새로운 movie 를 생성해야하는 번거로움이 있다.

간단하게 해결 가능하다. `beforeEach`를 `beforeAll`로 바꿔주자. 그럼 테스트를 진행하며 `POST`했던 요소를 기억한다.

<br>

---

### 2.

테스트를 할 때 생성하는 app과 실제 프로그램이 생성하는 app이 다르다는 것을 인지해야한다.

app 생성 부분을 보자.

실제 프로그램은 다음과 같다.

```ts
const app = await NestFactory.create(AppModule);
app.useGlobalPipes(
  new ValidationPipe({
    whitelist: true,
    forbidNonWhitelisted: true, // 정의되지 않은 키가 들어오면 에러
    transform: true,
  }),
);
await app.listen(3000);
```

테스트 프로그램은 다음과 같다.

```ts
beforeAll(async () => {
  ...
  app = moduleFixture.createNestApplication();
  await app.init();
});
```

어떤 차이가 있는지 보이는가?? 테스트 프로그램에서는 `Pipe` 검사에 관한 옵션이 없다. 이러면 테스트를 할 때 실제 프로그램과 차이를 보일 수 있다. 그렇기 때문에 테스트 프로그램의 app을 실제 프로그램과 같게 바꿔줘야한다.

```ts
...
app = moduleFixture.createNestApplication();
app.useGlobalPipes(
  new ValidationPipe({
    whitelist: true,
    forbidNonWhitelisted: true, // 정의되지 않은 키가 들어오면 에러
    transform: true,
  }),
);
await app.init();
```

<br>

---

### 3. 다양한 테스트를 해보자!!

```ts
describe('/movies/:id', () => {
  it('GET 200', () => {
    return request(app.getHttpServer()).get('/movies/1').expect(200);
  });
  it('GET 404', () => {
    return request(app.getHttpServer()).get('/movies/999').expect(404);
  });
  it('PATCH 200', () => {
    return request(app.getHttpServer())
      .patch('/movies/1')
      .send({ title: 'Updated Test' })
      .expect(200);
  });
  it('DELETE 200', () => {
    return request(app.getHttpServer()).delete('/movies/1').expect(200);
  });
});
```
