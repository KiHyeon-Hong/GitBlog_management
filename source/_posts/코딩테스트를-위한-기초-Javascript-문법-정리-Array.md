---
title: 코딩테스트를 위한 기초 Javascript 문법 정리 Array
date: 2021-12-02 21:35:57
tags:
  - Coding test
  - javascript
categories:
  - Coding test
  - Javascript
---

## 코딩테스트에서 자주 사용하는 Array methods (참고자료)

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array
- 여러 메소드의 기초 사용법을 유형별로 정리한다.

## 데이터 반환 (특정 인덱스)

### at

- 해당 인덱스의 요소를 반환한다.
- .at(-1)을 사용할 수 있다.

```javascript
let arr = ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10'];
console.log(arr.at(1));
// 2
console.log(arr.at(2));
// 3
console.log(arr.at(-1));
// 10
```

#### 다른 메소드와 비교

```javascript
const colors = ['빨강', '초록', '파랑'];
// length 속성 사용
const lengthWay = colors[colors.length - 2];
console.log(lengthWay); // '초록' 기록
// slice() 메서드 사용. 배열을 반환함에 주의
const sliceWay = colors.slice(-2, -1);
console.log(sliceWay[0]);
// at() 메서드 사용
const atWay = colors.at(-2);
console.log(atWay);
```

## 데이터 추가 및 삭제 (Stack과 Queue)

### pop

- 배열에서 마지막 요소를 제거하고 그 요소를 반환한다.

```javascript
const plants = ['broccoli', 'cauliflower', 'cabbage', 'kale', 'tomato'];
console.log(plants.pop());
// expected output: "tomato"
console.log(plants);
// expected output: ["broccoli", "cauliflower", "cabbage", "kale"]
plants.pop();
console.log(plants);
// expected output: ["broccoli", "cauliflower", "cabbage"]
```

### push

- 배열의 끝에 하나 이상의 요소를 추가하고, 배열의 길이를 반환한다.

```javascript
const animals = ['pigs', 'goats', 'sheep'];
const count = animals.push('cows');
console.log(count);
// expected output: 4
console.log(animals);
// expected output: Array ["pigs", "goats", "sheep", "cows"]
animals.push('chickens', 'cats', 'dogs');
console.log(animals);
// expected output: Array ["pigs", "goats", "sheep", "cows", "chickens", "cats", "dogs"]
```

### shift

- 배열에서 첫번째 요소를 제거하고, 제거된 요소를 반환한다.

```javascript
const array1 = [1, 2, 3];
const firstElement = array1.shift();
console.log(array1);
// expected output: [2, 3]
console.log(firstElement);
// expected output: 1
```

### unshift

- 새로운 요소를 배열의 맨 앞쪽에 추가한다.

```javascript
const array1 = [1, 2, 3];
console.log(array1.unshift(4, 5));
// expected output: 5
console.log(array1);
// expected output: Array [4, 5, 1, 2, 3]
```

## 데이터 탐색 (조건문)

### some

- 배열 안의 어떤 요소라도 주어진 판별식을 통과하는 지 테스트한다.

```javascript
const array = [1, 2, 3, 4, 5];
// checks whether an element is even
const even = (element) => element % 2 === 0;
console.log(array.some(even));
// expected output: true
```

### every

- 배열 안의 모든 요소가 주어진 판별 함수를 통과하는 지 테스트한다.
- 거짓을 반환하는 요소를 찾을 때까지 배열에 있는 각 요소에 대해 1번씩 실행한다.

```javascript
const isBelowThreshold = (currentValue, index, array) => currentValue < 40;
const array1 = [1, 30, 39, 29, 10, 13];
console.log(array1.every(isBelowThreshold));
// expected output: true
```

### includes

- 배열이 특정 요소를 포함하고 있는지 판별한다.

```javascript
const array1 = [1, 2, 3];

console.log(array1.includes(2));
// expected output: true
const pets = ['cat', 'dog', 'bat'];
console.log(pets.includes('cat'));
// expected output: true
console.log(pets.includes('at'));
// expected output: false
```

- 탐색을 시작할 위치를 지정할 수 있다.

```javascript
[1, 2, 3].includes(2); // true
[1, 2, 3].includes(4); // false
[1, 2, 3].includes(3, 3); // false
[1, 2, 3].includes(3, -1); // true
[1, 2, NaN].includes(NaN); // true
```

## 데이터 반환 (조건문)

### find

- 주어진 판별식을 만족하는 첫번째 요소의 값을 반환한다.

```javascript
const array1 = [5, 12, 8, 130, 44];
const found = array1.find((element) => element > 10);
console.log(found);
// expected output: 12
```

### findIndex

- 판별식을 만족하는 첫번째 요소에 대한 인덱스를 반환한다.

```javascript
const array1 = [5, 12, 8, 130, 44];
const isLargeNumber = (element) => element > 13;
console.log(array1.findIndex(isLargeNumber));
// expected output: 3
```

### indexOf

- 배열에서 지정된 요소를 찾을 수 있는 첫번째 인덱스를 반환하며, 없다면 -1을 반환한다.

```javascript
const beasts = ['ant', 'bison', 'camel', 'duck', 'bison'];
console.log(beasts.indexOf('bison'));
// expected output: 1
// start from index 2
console.log(beasts.indexOf('bison', 2));
// expected output: 4
console.log(beasts.indexOf('giraffe'));
// expected output: -1
```

- 탐색을 시작할 위치를 지정할 수 있다.

```javascript
var array = [2, 9, 9];
array.indexOf(2); // 0
array.indexOf(7); // -1
array.indexOf(9, 2); // 2
array.indexOf(2, -1); // -1
array.indexOf(2, -3); // 0
```

### lastIndexOf

- 배열에서 주어진 값을 찾을 수 있는 마지막 인덱스를 반환하며, 없다면 -1을 반환한다.

```javascript
const animals = ['Dodo', 'Tiger', 'Penguin', 'Dodo'];
console.log(animals.lastIndexOf('Dodo'));
// expected output: 3
console.log(animals.lastIndexOf('Tiger'));
// expected output: 1
```

## 배열 구조 변경

### concat

- 기존 배열을 변경하지 않으며, 추가된 새로운 배열을 반환한다.

```javascript
const array1 = ['a', 'b', 'c'];
const array2 = ['d', 'e', 'f'];
const array3 = array1.concat(array2); // array1.concat(array2, array3, array4); 가능
console.log(array3);
// expected output: ["a", "b", "c", "d", "e", "f"]
```

### flat

- 모든 하위 배열 요소를 지정한 깊이까지 재귀적으로 이어붙인 새로운 배열을 생성한다.

```javascript
const arr1 = [1, 2, [3, 4]];
arr1.flat();
// [1, 2, 3, 4]
const arr2 = [1, 2, [3, 4, [5, 6]]];
arr2.flat();
// [1, 2, 3, 4, [5, 6]]
const arr3 = [1, 2, [3, 4, [5, 6]]];
arr3.flat(2);
// [1, 2, 3, 4, 5, 6]
const arr4 = [1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]];
arr4.flat(Infinity);
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
const arr5 = [1, 2, , 4, 5]; // 빈 칸 제거 기능도 있다.
arr5.flat();
// [1, 2, 4, 5]
```

### flatMap

- 매핑함수를 사용해 각 엘리먼트에 대해 map을 수행 후, 결과를 새로운 배열로 평탄화 한다.

```javascript
let arr1 = [1, 2, 3, 4];
arr1.map((x) => [x * 2]);
// [[2], [4], [6], [8]]
arr1.flatMap((x) => [x * 2]);
// [2, 4, 6, 8]
// 한 레벨만 평탄화됨
arr1.flatMap((x) => [[x * 2]]);
// [[2], [4], [6], [8]]
```

## 데이터 변경

### fill

- 배열의 시작부터 끝까지 정적인 값 하나로 채운다.

```javascript
const array1 = [1, 2, 3, 4, 5, 6];
// fill with 0 from position 2 until position 4
console.log(array1.fill(0, 2, 4));
// expected output: [1, 2, 0, 0, 5, 6]
// fill with 5 from position 1
console.log(array1.fill(5, 1));
// expected output: [1, 5, 5, 5, 5, 5]
console.log(array1.fill(6));
// expected output: [6, 6, 6, 6, 6, 6]
```

### slice

- 특정 배열의 처음부터 끝까지 얕은 복사하여 새로운 배열로 반환한다.

```javascript
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];
console.log(animals.slice(2));
// expected output: Array ["camel", "duck", "elephant"]
console.log(animals.slice(2, 4));
// expected output: Array ["camel", "duck"]
console.log(animals.slice(1, 5));
// expected output: Array ["bison", "camel", "duck", "elephant"]
console.log(animals.slice(-2));
// expected output: Array ["duck", "elephant"]
console.log(animals.slice(2, -1));
// expected output: Array ["camel", "duck"]
console.log(animals.slice());
// expected output: Array ["ant", "bison", "camel", "duck", "elephant"]
```

### splice

- 배열의 기존 요소를 삭제 또는 교체하거나 새 요소를 추가하여 배열의 내용을 변경한다.

```javascript
const months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
// inserts at index 1
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "June"]
months.splice(4, 1, 'May');
// replaces 1 element at index 4
console.log(months);
// expected output: Array ["Jan", "Feb", "March", "April", "May"]
```

### sort

- 기본 정렬 순서는 문자열의 유니코드 코드 포인트를 따른다.

```javascript
const months = ['March', 'Jan', 'Feb', 'Dec'];
months.sort();
console.log(months);
// expected output: Array ["Dec", "Feb", "Jan", "March"]

const array1 = [1, 30, 4, 21, 100000];
array1.sort();
console.log(array1);
// expected output: Array [1, 100000, 21, 30, 4]
```

```javascript
function compare(a, b) {
  if (a is less than b by some ordering criterion) {
    return -1;
  }
  if (a is greater than b by the ordering criterion) {
    return 1;
  }
  // a must be equal to b
  return 0;
}
```

### reverse

- 배열의 순서를 반전한다.

```javascript
const array1 = ['one', 'two', 'three'];
console.log('array1:', array1);
// expected output: "array1:" ["one", "two", "three"]
const reversed = array1.reverse();
console.log('reversed:', reversed);
// expected output: "reversed:" ["three", "two", "one"]
// Careful: reverse is destructive -- it changes the original array.
console.log('array1:', array1);
// expected output: "array1:" ["three", "two", "one"]
```

## 배열로 변경, 혹은 배열을 변경

### from

- 유사 배열 객체나 반복 가능한 객체를 얕게 복사해 새로운 Array를 만든다.

```javascript
console.log(Array.from('foo'));
// expected output: ["f", "o", "o"]
console.log(Array.from([1, 2, 3], (x) => x + x));
// expected output: [2, 4, 6]
```

- Set에서 배열 만들기

```javascript
const s = new Set(['foo', window]);
Array.from(s);
// ["foo", window]
```

### join

- 배열의 모든 요소를 연결해 하나의 문자열로 만든다.

```javascript
const elements = ['Fire', 'Air', 'Water'];
console.log(elements.join());
// expected output: "Fire,Air,Water"
console.log(elements.join(''));
// expected output: "FireAirWater"
console.log(elements.join('-'));
// expected output: "Fire-Air-Water"
```

### toString

- 지정된 배열 및 요소를 나타내는 문자열을 반환한다.

```javascript
const array1 = [1, 2, 'a', '1a'];

console.log(array1.toString());
// expected output: "1,2,a,1a"
```

## 배열 데이터 반복

### map

- 배열 내의 모든 요소 각각에 대해 주어진 함수를 호출한 결과를 모아 새로운 배열로 반환한다.

```javascript
const array1 = [1, 4, 9, 16];
const map1 = array1.map((x, index, array) => x * 2);
console.log(map1);
// expected output: [2, 8, 18, 32]
```

### filter

- 주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환한다.

```javascript
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];
const result = words.filter((word, index, arr) => word.length > 6);
console.log(result);
// expected output: ["exuberant", "destruction", "present"]
```

## reduce

- 각 요소에 대해 주어진 함수를 실행하고, 하나의 결과 값을 반환한다.

```javascript
const array1 = [1, 2, 3, 4];
const reducer = (previousValue, currentValue) => previousValue + currentValue;
// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10
// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
```
