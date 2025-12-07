---
title: "🦆 Understanding Structural Typing in TypeScript (with Java Comparison)"
lang: "en"
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

In TypeScript, **Structural Typing** is one of the most fundamental concepts for type compatibility.  

If you've worked with Java or other statically typed languages before, this may feel very different from the traditional approach.

This post explains:

- What Structural Typing is
- How it relates to Duck Typing
- How it differs from Java's Nominal Typing
- Pros and cons with examples

---

## 🧠 What Is Structural Typing?

**Structural Typing** means that **type compatibility is determined by the structure (shape) of the type**, not by its name.

In TypeScript, two types are considered compatible if they contain the **same required properties and methods**, regardless of whether they were declared with the same interface or class name.

### ✔ Example

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

Even though person has extra fields (city), it matches the required structure of User, so the assignment is allowed.

---

## 🦆 Structural Typing and Duck Typing

The idea is closely related to Duck Typing:

> "If it walks like a duck and quacks like a duck, it's a duck."

In programming terms:

> If an object has the required properties, it can be treated as that type.

```js
function printName(obj) {
  console.log(obj.name);
}

printName({ name: "Coco" }); // works fine
```

JavaScript naturally follows Duck Typing at runtime.

TypeScript applies the same idea at compile time via Structural Typing.

---

## ☕ Structural Typing vs Java's Nominal Typing

Languages like Java, C#, and Kotlin use **Nominal Typing**, where type compatibility is determined by the declared name of the type (class or interface).

### Example in Java

```java
class User {
    String name;
    int age;
}

class Person {
    String name;
    int age;
}

User u = new Person(); // ❌ Compile error
```

Even though User and Person have identical fields, Java disallows assignment because the types are not explicitly related.

### 📌 Key Differences

| Concept               | TypeScript (Structural)               | Java (Nominal)                   |
| --------------------- | ------------------------------------- | -------------------------------- |
| Type compatibility    | Based on structure (fields & methods) | Based on declared type name      |
| Flexibility           | High                                  | Low                              |
| Safety                | Lower                                 | Higher                           |
| Suitable for          | API integration / JS ecosystem        | Large, strict enterprise systems |
| Extra fields allowed? | Yes                                   | No                               |

---

## 🎯 Why TypeScript Uses Structural Typing

- Seamlessly interoperates with JavaScript, which is inherently dynamic
- Perfect for API data handling and loosely structured objects
- Encourages interface-driven development instead of inheritance hierarchies

---

## ⚠ Potential Pitfall Example

```ts
interface Point {
  x: number;
  y: number;
}

function move(p: Point) {
  console.log(p.x + p.y);
}

const weird = { x: 10, y: 20, z: 99 };
move(weird); // OK but unintended object can pass through
```

Structural typing is flexible, but sometimes too permissive.

---

## 🧾 Summary

- **Structural Typing**: type compatibility based on shape, not name
- **Duck Typing**: runtime concept based on object capabilities
- **TypeScript** uses Structural Typing at compile time to align with JavaScript's behavior
- **Java** uses Nominal Typing, requiring explicit type names or inheritance relationships

---

## 📍 One-sentence Summary

TypeScript considers types equal if they look the same, while Java considers them equal only if they are explicitly declared as the same.

