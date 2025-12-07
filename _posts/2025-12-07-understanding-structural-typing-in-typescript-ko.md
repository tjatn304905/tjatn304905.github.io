---
title: "🦆 TypeScript의 구조적 타이핑 이해하기 (Java와 비교)"
lang: "ko"
categories:
  - TypeScript
  - Programming
tags:
  - TypeScript
  - Structural Typing
  - Java
  - Duck Typing
  - Type System
---

TypeScript에서 **구조적 타이핑(Structural Typing)**은 타입 호환성을 결정하는 가장 기본적인 개념 중 하나입니다.

Java나 다른 정적 타입 언어를 사용해본 경험이 있다면, 이는 전통적인 접근 방식과 매우 다르게 느껴질 수 있습니다.

이 게시물에서는 다음을 설명합니다:

- 구조적 타이핑이 무엇인지
- Duck Typing과의 관계
- Java의 명목적 타이핑(Nominal Typing)과의 차이점
- 예시와 함께 장단점

---

## 🧠 구조적 타이핑이란?

**구조적 타이핑**은 **타입 호환성이 타입의 이름이 아닌 구조(모양)에 의해 결정**된다는 것을 의미합니다.

TypeScript에서는 두 타입이 같은 인터페이스나 클래스 이름으로 선언되었는지와 관계없이, **필수 속성과 메서드가 동일**하면 호환되는 것으로 간주됩니다.

### ✔ 예제

```ts
interface User {
  name: string;
  age: number;
}

const person = {
  name: "Tom",
  age: 25,
  city: "Seoul"
};

const u: User = person; // OK
```

person에 추가 필드(city)가 있더라도, User의 필수 구조와 일치하므로 할당이 허용됩니다.

---

## 🦆 구조적 타이핑과 Duck Typing

이 개념은 Duck Typing과 밀접한 관련이 있습니다:

> "오리처럼 걷고 오리처럼 꽥꽥거리면, 그것은 오리다."

프로그래밍 용어로 표현하면:

> 객체가 필수 속성을 가지고 있다면, 해당 타입으로 취급할 수 있다.

```js
function printName(obj) {
  console.log(obj.name);
}

printName({ name: "Coco" }); // 잘 작동함
```

JavaScript는 런타임에 자연스럽게 Duck Typing을 따릅니다.

TypeScript는 컴파일 타임에 구조적 타이핑을 통해 동일한 개념을 적용합니다.

---

## ☕ 구조적 타이핑 vs Java의 명목적 타이핑

Java, C#, Kotlin과 같은 언어는 **명목적 타이핑(Nominal Typing)**을 사용하며, 타입 호환성은 타입(클래스 또는 인터페이스)의 선언된 이름에 의해 결정됩니다.

### Java 예제

```java
class User {
    String name;
    int age;
}

class Person {
    String name;
    int age;
}

User u = new Person(); // ❌ 컴파일 오류
```

User와 Person이 동일한 필드를 가지고 있더라도, Java는 타입이 명시적으로 관련되지 않았기 때문에 할당을 허용하지 않습니다.

### 📌 주요 차이점

| 개념               | TypeScript (구조적)               | Java (명목적)                   |
| --------------------- | ------------------------------------- | -------------------------------- |
| 타입 호환성    | 구조 기반 (필드 & 메서드) | 선언된 타입 이름 기반      |
| 유연성           | 높음                                  | 낮음                              |
| 안전성                | 낮음                                 | 높음                           |
| 적합한 용도          | API 통합 / JS 생태계        | 대규모, 엄격한 엔터프라이즈 시스템 |
| 추가 필드 허용? | 예                                   | 아니오                               |

---

## 🎯 TypeScript가 구조적 타이핑을 사용하는 이유

- 본질적으로 동적인 JavaScript와 원활하게 상호 운용
- API 데이터 처리 및 느슨하게 구조화된 객체에 완벽
- 상속 계층 구조 대신 인터페이스 기반 개발을 장려

---

## ⚠ 잠재적 함정 예제

```ts
interface Point {
  x: number;
  y: number;
}

function move(p: Point) {
  console.log(p.x + p.y);
}

const weird = { x: 10, y: 20, z: 99 };
move(weird); // OK이지만 의도하지 않은 객체가 통과할 수 있음
```

구조적 타이핑은 유연하지만, 때로는 너무 관대할 수 있습니다.

---

## 🧾 요약

- **구조적 타이핑**: 이름이 아닌 모양에 기반한 타입 호환성
- **Duck Typing**: 객체의 능력에 기반한 런타임 개념
- **TypeScript**는 JavaScript의 동작과 일치시키기 위해 컴파일 타임에 구조적 타이핑을 사용
- **Java**는 명목적 타이핑을 사용하여 명시적인 타입 이름이나 상속 관계를 요구

---

