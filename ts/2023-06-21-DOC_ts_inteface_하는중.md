---
title: "[DOCS] TS"
categories:
    - Type Script
tags:
    - typescript

last_modified_at: 2023-06-06T15:50:58
---

[Object Types](https://www.typescriptlang.org/docs/handbook/2/objects.html?) 페이지 해석

자바스크립트에서 데이터를 그룹화하고 전달하는 기본 방식은 `객체`를 사용하는 것입니다. 타입스크립트에서는 객체 유형을 통해 이를 표현합니다.

앞서 살펴본 것처럼 익명이 될 수도 있습니다.

```ts
function greet(person: { name: string; age: number }) {
    return "Hello " + person.name;
}
```

또는 interface를 사용하여 이름을 지정할 수 있습니다.

```ts
interface Person {
    name: string;
    age: number;
}

function greet(person: Person) {
    return "Hello " + person.name;
}
```

또는 type alias 를 사용할 수 있습니다.

```ts
type Person = {
    name: string;
    age: number;
};

function greet(person: Person) {
    return "Hello " + person.name;
}
```

위의 세 가지 예제 모두에서 속성 `name`(`string`이어야 함)과 `age`(`number`이어야 함)가 포함된 객체를 받는 함수를 작성했습니다.

<br>

---

## Quick Reference

중요한 구문을 한 눈에 빠르게 살펴보고 싶다면 유형과 인터페이스 모두에 대한 치트 시트가 준비되어 있습니다.

### ↘︎ Classes

<img src="https://github.com/Gaepo-transcendance-fighters/ft_memo/assets/85930183/a95403e9-78c4-46db-8681-15fc02ad4b2d" width="90%">

<br>

### ↘︎ Control Flow Analysis

<img src="https://github.com/Gaepo-transcendance-fighters/ft_memo/assets/85930183/ce66a5f9-215f-4051-bf56-6ed289223022" width="90%">

<br>

### ↘︎ Interfaces

<img src="https://github.com/Gaepo-transcendance-fighters/ft_memo/assets/85930183/00a35100-0898-40a8-93bc-dbb6513292d4" width="90%">

<br>

### ↘︎ Types

<img src="https://github.com/Gaepo-transcendance-fighters/ft_memo/assets/85930183/6366b2ae-ab31-4bbc-b779-0fa4f84ed3ec" width="90%">

<br>

---

## Property Modifiers

객체의 각 프로퍼티는 유형, 프로퍼티가 optional 인지 여부, 프로퍼티에 쓸 수 있는지 여부 등 두 가지를 지정할 수 있습니다.

<br>

### Optional Properties

대부분의 경우 프로퍼티 세트가 있을 수 있는 객체를 다루게 됩니다. 이러한 경우 이름 끝에 물음표(?)를 추가하여 해당 속성을 선택 사항으로 표시할 수 있습니다.

```ts
interface PaintOptions {
    shape: Shape;
    xPos?: number;
    yPos?: number;
}

function paintShape(opts: PaintOptions) {
    // ...
}

const shape = getShape();
paintShape({ shape });
paintShape({ shape, xPos: 100 });
paintShape({ shape, yPos: 100 });
paintShape({ shape, xPos: 100, yPos: 100 });
```

이 예제에서는 `xPos`와 `yPos` 모두 선택 사항으로 간주됩니다. 둘 중 하나를 제공하도록 선택할 수 있으므로 위의 paintShape에 대한 모든 호출은 유효합니다. 옵션이 의미하는 것은 프로퍼티가 설정된 경우 특정 type 을 갖는 것이 좋다는 것입니다.

또한 프로퍼티에서 읽을 수도 있다. 하지만 [strictNullChecks](https://www.typescriptlang.org/tsconfig#strictNullChecks)에서 해당 프로퍼티가 `undefined` 일 가능성이 있다고 알려줍니다.

```ts
function paintShape(opts: PaintOptions) {
  let xPos = opts.xPos;

(property) PaintOptions.xPos?: number | undefined
  let yPos = opts.yPos;

(property) PaintOptions.yPos?: number | undefined
  // ...
}
```

자바스크립트에서는 프로퍼티가 설정된 적이 없더라도 프로퍼티에 액세스할 수 있으며, `undefined` 만 제공할 뿐입니다. 우리는 정의되지 않은 값을 확인하여 특별히 처리하면 됩니다.

```js
function paintShape(opts: PaintOptions) {
    let xPos = opts.xPos === undefined ? 0 : opts.xPos;

    let xPos: number;
    let yPos = opts.yPos === undefined ? 0 : opts.yPos;

    let yPos: number;
    // ...
}
```

지정되지 않은 값에 대해 기본값을 설정하는 이러한 패턴은 매우 일반적이어서 자바스크립트에는 이를 지원하는 구문이 있습니다.

```js
function paintShape({ shape, xPos = 0, yPos = 0 }: PaintOptions) {
  console.log("x coordinate at", xPos);

(parameter) xPos: number
  console.log("y coordinate at", yPos);

(parameter) yPos: number
  // ...
}
```

여기서는 `paintShape` 매개변수에 [구조 분해 할당](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)을 사용했고, `xPos`와 `yPos`에 기본값을 제공했습니다. 이제 `xPos`와 `yPos`는 `paintShape` 본문에 확실히 존재하지만, `paintShape`를 호출하는 모든 호출자에게는 선택 사항입니다.

현재 구조 분해 발당에 타입을 설정할 수 있는 방법은 없습니다. 다음 구문은 자바스크립트에서 이미 다른 의미를 갖기 때문입니다.

```ts
function draw({ shape: Shape, xPos: number = 100 /*...*/ }) {
  render(shape);
❗️ Cannot find name 'shape'. Did you mean 'Shape'?
  render(xPos);
❗️ Cannot find name 'xPos'.
}
```

객체 분해 할당에서 `shape: Shape`는 "속성 `shape` 을 가져와서 로컬에서 `Shape` 라는 변수로 재정의한다"는 의미입니다. 마찬가지로 `xPos: number`는 매개변수의 `xPos`에 기반한 값을 가진 `number`라는 변수를 생성합니다.

[mapping modifiers](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html#mapping-modifiers) 를 사용하여 `optional` 속성을 제거할 수 있습니다.

<br>

### readonly Properties
