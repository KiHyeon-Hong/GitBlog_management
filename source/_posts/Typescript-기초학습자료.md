---
title: Typescript 기초학습자료
date: 2022-02-03 20:21:40
tags:
  - typescript
categories:
  - Typescript
---

## 기본 타입과 커스텀 타입

### 기본적인 타입 표기

```typescript
let a: string;
let b: number;
```

### 타입스크립트에서 제공하는 타입들

- string: 문자열
- boolean: true, false
- number: 숫자
- symbol: Symbol 생성자를 호출해 생성된 고유한 값
- any: 모든 타입을 허용
- unknown: any와 비슷하나, 먼저 타입을 지정하거나 좁히지 않으면 조작이 불가능
- never: 도달할 수 없는 코드
- void: 값이 없음

#### 명시적 타입 주의사항

- 변수의 타입은 이미 문자열이므로 타입스크립트는 string으로 유추할 수 있다.
- 따라서, n2와 같이 컴파일러가 유추할 수 있는 곳에 다시 타입을 지정할 필요가 없다.

```typescript
let n1 = 'AAA;';
let n2: string = 'BBB';
```

- 초기값 없이 변수를 선언하면 타입스크립트는 any로 유추한다.

```typescript
let product; // any
```

### 유니온 타입

- or 연산자와 같이 변수에 지정할 수 있는 타입이 여러 개인 경우에 사용한다.

```typescript
function padLeft(value: string, padding: any) {
  if (typeof padding === 'number') {
    return Array(padding + 1).join(' ') + value;
  }
  if (typeof padding === 'string') {
    return padding + value;
  }
  throw new Error(`Expected string or number, got '${padding}'.`);
}

console.log(padLeft('Hello world', 4)); // returns "    Hello world"
console.log(padLeft('Hello world', ' Yakov says ')); // returns "  Yakov says  Hello world"
console.log(padLeft('Hello world', true)); // if padding had type any - runtime error
```

```typescript
function padLeft(value: string, padding: string | number) {
  if (typeof padding === 'number') {
    return Array(padding + 1).join(' ') + value;
  }
  if (typeof padding === 'string') {
    return padding + value;
  }
  throw new Error(`Expected string or number, got '${padding}'.`);
}

console.log(padLeft('Hello world', 4)); // returns "    Hello world"
console.log(padLeft('Hello world', ' Yakov says ')); // returns "  Yakov says  Hello world"
console.log(padLeft('Hello world', true)); // if padding had type any - compile error
```

#### typeof, instanceof

- typeof는 typescript 내장 타입에 사용하며, instanceof는 사용자가 만든 타입에 사용한다.

```typescript
if (person instanceof Person) {
}
```

### 커스텀 타입

- ?는 해당 프로퍼티가 필수가 아닌 경우에 입력한다.

```typescript
type age = number;

type Person = {
  age: number;
  name: string;
  weight?: number;
};
```

```typescript
let person: Person = {
  age: 19,
  name: 'AAA',
};
```

### 접근 제한자

- 타입스크립트에는 readonly, private, protected, public 키워드가 있다.
- readonly는 const와 비슷하지만, 클래스 프로퍼티에 사용할 수 없다.

```typescript
class Block {
  readonly a: string;
  constructor(readonly b: number) {}
}
```

### 인터페이스 (interface, implements)

- 자바스크립트 코드로 컴파일 되지 않는다.
- 개발 도중 잘못된 타입을 피할 수 있게 도움을 준다.

```typescript
interface Person {
  firstName: string;
  lastName: string;
  age: number;
}
```

- class와 같이 new 키워드를 사용해 인스턴스화 시킬 수 있지만, 자바스크립트 코드에 해당 부분이 없다.
- 즉, 코드가 간결해진다.

#### type, interface, class

- 런타임동안 객체를 인스턴스화한다면 interface, type을 사용하며, 값을 나타내는 데에 사용할 경우에는 class를 사용한다.
- 타입스크립트의 타입 검사기로 안전하게 커스텀 타입을 선언하고자 할 때에는 type, interface를 사용하며, 이들은 자바스크립트로 컴파일되지 않기 때문에 런타임 용량이 작아진다.
- class는 자바스크립트 코드로 컴파일되기 때문에 용량이 커진다.
- type 키워드는 interface와 동일한 기능뿐만이 아니라 더 많은 기능을 사용할 수 있다. 예를 들어, interface는 합집합, 교집합 개념을 사용할 수 없지만, type은 가능하다.

### 구조적 타입 시스템과 명목적 타입 시스템

- 타입스크립트는 구조적 타입 시스템을 사용한다.
- Person과 Customer은 같은 구조를 갖고 있기 때문에 오류가 발생하지 않는다.

```typescript
class Person {
  name: string;
}
class Customer {
  name: string;
}
const cust: Customer = new Person();
```

```typescript
class Person {
  name: string;
  age: number;
}
class Customer {
  name: string;
}
const cust: Customer = new Person();
const per: Person = new Customer(); // Error
```

## 클래스와 인터페이스를 사용한 객체 지향 프로그래밍

### public, private, protected 접근 제어자

- public: 모든 내부 및 외부 클래스에서 접근 가능
- private: 클래스 내에서만 접근 가능
- protected: 동일 패키지에 속하는 클래스와 서브 클래스 관계일 경우에만 접근 가능

### super() 키워드 사용

- 슈퍼 클래스와 서브 클래스가 같은 이름의 메소드를 가지고 있다면, super() 메소드로 슈퍼 클래스의 생성자를 호출하여야 한다.

```typescript
class Person {
  contructor(public firstName: string, public lastName: string, private age: number) {}
}
class Employee extends Person {
  contructor(firstName: string, lastName: string, age: number, public department: string) {
    super(firstName, LastName, age);
  }
}
const empl = new Employee('A', 'B', 30, 'C');
```

### 추상 클래스

- 추상 클래스는 객체로 만들 수 없는 추상적인 개념으로 일종의 설계도이다.
- 인스턴스화 될 수 없다.
- 추상 메소드를 호출하는 명령은 사용할 수 없다. 추상 클래스는 인스턴스화될 수 없으므로, 추상 멤버는 절대로 호출되지 않는다.

```typescript
abstract class Person {
  contructor() {}
  abstract increasePay(percent: number): void;
}
```

### 메소드 오버로딩

- 타입스크립트에서는 1개의 메소드 구현을 갖는다.

```typescript
class ProductService {
  getProducts();
  getProducts(id: number);
  getProducts(id?: number) {
    // 모든 가능한 파라매터를 다루는 생성자를 구현한다.
    console.log(`call getProducts`);
  }
}
const proSevice = new ProductService();
proService.getProducts(123);
proService.getProducts();
```

### 인터페이스 사용

- 인터페이스로 클래스를 선언할 때, 인터페이스 내 각 메소드를 구현해야 한다.

#### 인터페이스 확장

```typescript
interface A {}
interface B extends A {}
```

## 열거타입(Enum)과 제네릭(Generic)

### 열거타입(Enum)

```typescript
enum Weekdays {
  Monday = 1,
  Tuesday, // 2
  Wednesday, // 3
  Thursday, // 4
  Friday, // 5
  Saturday, // 6
  Sunday, // 7
}
```

- 열거 타입 멤버에 할당된 숫자를 신경 쓰지 않아도 되는 경우가 있다.

```typescript
enum Alpha {
  A,
  B,
}

function aOrB(alpha: Alpha): void {} // A, B 외의 문자가 들어올 위험이 없다.
function aOrB(alpha: string): void {} // A, B 외의 문자가 들어올 위험이 있다.
```

#### 문자열 열거

```typescript
enum Direction {
  Up = 'UP',
  Down = 'DOWN',
  Left = 'LEFT',
  Right = 'RIGHT',
}

move(where:string)  // move('North') Error
move(where:Direction) // move(Direction.Up)
```

- 커스텀 타입을 이용하는 방법

```typescript
type Direction = 'Up' | 'Down' | 'Left' | 'Right';
function move(direction: Direction) {}
```

#### const enum

- const enum은 자바스크립트가 생성되지 않는다.

### 제네릭(Generic)

- 제네릭을 사용하면 함수의 호출자가 나중에 구체적인 타입을 지정할 수 있다.

```typescript
class Person {}
const people = new Array<Person>(10);
```

### 제네릭 타입 생성

```typescript
interface Comp<T> {
  compTo(value: T): number;
}
class Rectangle implements Comp<Rectangle> {
  compTo(value: Rectangle): number {}
}
class Triangle implements Comp<Triangle> {
  compTo(value: Triangle): number {}
}
```

### 고차함수 내 반환 타입 강제

- 함수를 파라매터로 받거나 다른 함수를 반환하는 함수를 고차함수라고 한다.

```typescript
const outerFunc = (someValue: number) => (multiplier: number) => someValue * multiplier;
const innerFunc = outerFunc(10);
let result = innerFunc(5);
console.log(result); //50
```

```typescript
const outerFunc = (someValue: number) => (multiplier: number) => someValue * multiplier;
const innerFunc = outerFunc(10);
let result = innerFunc(5);
console.log(result); //50
```

## 참고자료

- 기초부터 블록체인 실습까지 단숨에 배우는 타입스크립트, 영진닷컴, 야코프 페인
