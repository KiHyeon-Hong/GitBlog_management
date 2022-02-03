---
title: 코딩테스트를 위한 기초 Javascript 문법 정리 Math
date: 2022-02-03 12:11:07
tags:
  - Coding test
  - javascript
categories:
  - Coding test
  - Javascript
---

## 코딩테스트에서 자주 사용하는 Math methods (참고자료)

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math
- 여러 메소드의 기초 사용법을 유형별로 정리한다.

## Properties

### Math.E

- 자연로그의 밑 값 e를 나타내며, 약 2.718이다.

```javascript
function compoundOneYear(interestRate, currentVal) {
  return currentVal * Math.E ** interestRate;
}
console.log(Math.E);
// expected output: 2.718281828459045
console.log((1 + 1 / 1000000) ** 1000000);
// expected output: 2.718280469 (approximately)
console.log(compoundOneYear(0.05, 100));
// expected output: 105.12710963760242
```

### Math.LN10

- 10의 자연로그 값, 약 2.302의 값이다.

```javascript
function getNatLog10() {
  return Math.LN10;
}
console.log(getNatLog10());
// expected output: 2.302585092994046
```

### Math.LN2

- 2의 자연로그 값, 약 0.693의 값이다.

```javascript
function getNatLog2() {
  return Math.LN2;
}
console.log(getNatLog2());
// expected output: 0.6931471805599453
```

### Math.LOG10E

- e의 로그 10 값, 약 0.434의 값이다.

```javascript
function getLog10e() {
  return Math.LOG10E;
}
console.log(getLog10e());
// expected output: 0.4342944819032518
```

### Math.LOG2E

- e의 로그 2 값, 약 1.442의 값이다.

```javascript
function getLog2e() {
  return Math.LOG2E;
}
console.log(getLog2e());
// expected output: 1.4426950408889634
```

### Math.PI

- 원의 둘레와 지름의 비율, 약 3.14159의 값이다.

```javascript
function calculateCircumference(radius) {
  return 2 * Math.PI * radius;
}
console.log(Math.PI);
// expected output: 3.141592653589793
console.log(calculateCircumference(10));
// expected output: 62.83185307179586
```

### Math.SQRT1_2

- 약 0.707의 값을 나타내는 루트 1/2이다.

```javascript
function getRoot1Over2() {
  return Math.SQRT1_2;
}
console.log(getRoot1Over2());
// expected output: 0.7071067811865476
```

### Math.SQRT2

- 2의 제곱근을 나타내고 약 1.414이다.

```javascript
function getRoot2() {
  return Math.SQRT2;
}
getRoot2(); // 1.4142135623730951
```

## Methods

### max

- 입력값으로 받은 0개 이상의 숫자 중 가장 큰 숫자를 반환한다.

```javascript
console.log(Math.max(1, 3, 2));
// expected output: 3
console.log(Math.max(-1, -3, -2));
// expected output: -1
const array1 = [1, 3, 2];
console.log(Math.max(...array1));
// expected output: 3
```

#### min

- 입력값으로 받은 0개 이상의 숫자 중 가장 작은 숫자를 반환한다.

### abs

- 주어진 숫자의 절댓값을 반환한다.

```javascript
function difference(a, b) {
  return Math.abs(a - b);
}
console.log(difference(3, 5));
// expected output: 2
console.log(difference(5, 3));
// expected output: 2
console.log(difference(1.23456, 7.89012));
// expected output: 6.6555599999999995
```

### pow

- base에 exponent를 제곱한 값을 반환한다.

```javascript
console.log(Math.pow(7, 3));
// expected output: 343
console.log(Math.pow(4, 0.5));
// expected output: 2
console.log(Math.pow(7, -2));
// expected output: 0.02040816326530612
//                  (1/49)
console.log(Math.pow(-7, 0.5));
// expected output: NaN
```

### sqrt

- 숫자의 제곱근을 반환한다.

```javascript
Math.sqrt(9); // 3
Math.sqrt(2); // 1.414213562373095
Math.sqrt(1); // 1
Math.sqrt(0); // 0
Math.sqrt(-1); // NaN
```

### cbrt

- 주어진 수의 세제곱근을 반환한다.

```javascript
Math.cbrt(NaN); // NaN
Math.cbrt(-1); // -1
Math.cbrt(-0); // -0
Math.cbrt(-Infinity); // -Infinity
Math.cbrt(0); // 0
Math.cbrt(1); // 1
Math.cbrt(Infinity); // Infinity
Math.cbrt(null); // 0
Math.cbrt(2); // 1.2599210498948734
```

### round

- 입력값을 반올림한 수와 가장 가까운 정수 값을 반환한다.

```javascript
console.log(Math.round(0.9));
// expected output: 1
console.log(Math.round(5.95), Math.round(5.5), Math.round(5.05));
// expected output: 6 6 5
console.log(Math.round(-5.05), Math.round(-5.5), Math.round(-5.95));
// expected output: -5 -5 -6
```

### ceil

- 주어진 숫자보다 크거나 같은 숫자 증 가장 작은 숫자를 integer로 반환한다.

```javascript
Math.ceil(0.95); // 1
Math.ceil(4); // 4
Math.ceil(7.004); // 8
Math.ceil(-0.95); // -0
Math.ceil(-4); // -4
Math.ceil(-7.004); // -7
```

### floor

- 주어진 숫자와 같거나 작은 정수 중에서 가장 큰 수를 반환한다.

```javascript
console.log(Math.floor(5.95));
// expected output: 5
console.log(Math.floor(5.05));
// expected output: 5
console.log(Math.floor(5));
// expected output: 5
console.log(Math.floor(-5.05));
// expected output: -6
```

### trunc

- 주어진 값의 소수부분을 제거하고 숫자의 정수부분을 반환한다.

```javascript
console.log(Math.trunc(13.37));
// expected output: 13
console.log(Math.trunc(42.84));
// expected output: 42
console.log(Math.trunc(0.123));
// expected output: 0
console.log(Math.trunc(-0.123));
// expected output: -0
```

```javascript
Math.trunc(13.37); // 13
Math.trunc(42.84); // 42
Math.trunc(0.123); //  0
Math.trunc(-0.123); // -0
Math.trunc('-1.123'); // -1
Math.trunc(NaN); // NaN
Math.trunc('foo'); // NaN
Math.trunc(); // NaN
```

### sign

- 주어진 수의 부호를 나타내는 +/-1을 반환한다.

```javascript
console.log(Math.sign(3));
// expected output: 1
console.log(Math.sign(-3));
// expected output: -1
console.log(Math.sign(0));
// expected output: 0
console.log(Math.sign('-3'));
// expected output: -1
```

### log2

```javascript
console.log(Math.log2(3));
// expected output: 1.584962500721156
console.log(Math.log2(2));
// expected output: 1
console.log(Math.log2(1));
// expected output: 0
console.log(Math.log2(0));
// expected output: -Infinity
```

### log10

```javascript
console.log(Math.log10(100000));
// expected output: 5
console.log(Math.log10(2));
// expected output: 0.3010299956639812
console.log(Math.log10(1));
// expected output: 0
console.log(Math.log10(0));
// expected output: -Infinity
```

### exp

- x를 인수로 하는 e^x 값을 반환한다.

```javascript
console.log(Math.exp(0));
// expected output: 1
console.log(Math.exp(1));
// expected output: 2.718281828459 (approximately)
console.log(Math.exp(-1));
// expected output: 0.36787944117144233
console.log(Math.exp(2));
// expected output: 7.38905609893065
```

### random

- 0 이상 1 미만의 구간에서 근사적으로 균일한(approximately uniform) 부동소숫점 의사난수를 반환한다.

```javascript
// 두 값 사이의 정수 난수 생성
function getRandomInt(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min)) + min; //최댓값은 제외, 최솟값은 포함
}
```
