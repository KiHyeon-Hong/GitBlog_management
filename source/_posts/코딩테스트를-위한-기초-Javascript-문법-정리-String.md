---
title: 코딩테스트를 위한 기초 Javascript 문법 정리 String
date: 2022-02-03 11:46:26
tags:
  - Coding test
  - javascript
categories:
  - Coding test
  - Javascript
---

## 코딩테스트에서 자주 사용하는 String methods (참고자료)

- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String
- 여러 메소드의 기초 사용법을 유형별로 정리한다.

## 문자열의 길이

### length

- 문자열의 길이를 나타낸다.

```javascript
const str = 'Life, the universe and everything. Answer:';
console.log(`${str} ${str.length}`);
// expected output: "Life, the universe and everything. Answer: 42"
```

## 특정 인덱스의 데이터 반환

### at

```javascript
const sentence = 'The quick brown fox jumps over the lazy dog.';
let index = 5;
console.log(`Using an index of ${index} the character returned is ${sentence.at(index)}`);
// expected output: "Using an index of 5 the character returned is u"
index = -4;
console.log(`Using an index of ${index} the character returned is ${sentence.at(index)}`);
// expected output: "Using an index of -4 the character returned is d"
```

### charAt

- 문자열에서 특정 인덱스에 위치하는 유니코드 단일문자를 반환한다.

```javascript
const sentence = 'The quick brown fox jumps over the lazy dog.';
const index = 4;
console.log(`The character at index ${index} is ${sentence.charAt(index)}`);
// expected output: "The character at index 4 is q"
```

### charCodeAt

- 주어진 인덱스에 대한 UTF-16 코드를 나타내는 0 ~ 65535 사이의 정수를 반환한다.

```javascript
const sentence = 'The quick brown fox jumps over the lazy dog.';
const index = 4;
console.log(`The character code ${sentence.charCodeAt(index)} is equal to ${sentence.charAt(index)}`);
// expected output: "The character code 113 is equal to q"
```

## 문자열 병합

### concat

- 매개변수로 전달된 모든 문자열을 호출 문자열에 붙인 새로운 문자열을 반환한다.

```javascript
const str1 = 'Hello';
const str2 = 'World';
console.log(str1.concat(' ', str2));
// expected output: "Hello World"
console.log(str2.concat(', ', str1));
// expected output: "World, Hello"
```

## 문자열 탐색 (조건문)

### startsWith

- 어떤 문자열이 특정 문자로 시작하는 지 확인하여 결과를 true 또는 false로 반환한다.
- 탐색을 시작할 위치를 지정할 수 있다.

```javascript
var str = 'To be, or not to be, that is the question.';
console.log(str.startsWith('To be')); // true
console.log(str.startsWith('not to be')); // false
console.log(str.startsWith('not to be', 10)); // true
```

### endsWith

- 어떤 문자열에서 특정 문자열로 끝나는지를 확인한다.

```javascript
var str = 'To be, or not to be, that is the question.';
console.log(str.endsWith('question.')); // true
console.log(str.endsWith('to be')); // false
console.log(str.endsWith('to be', 19)); // true, 19는 찾고자하는 문자열의 길이값이며, 기본값은 문자열 전체길이이다.
```

### includes

- 하나의 문자열이 다른 문자열에 포함되어 있는지를 판별하고, 결과를 true 또는 false로 반환한다.
- 대소문자를 구분한다.

```javascript
const sentence = 'The quick brown fox jumps over the lazy dog.';
const word = 'fox';
console.log(`The word "${word}" ${sentence.includes(word) ? 'is' : 'is not'} in the sentence`);
// expected output: "The word "fox" is in the sentence"
```

```javascript
var str = 'To be, or not to be, that is the question.';
console.log(str.includes('To be')); // true
console.log(str.includes('question')); // true
console.log(str.includes('nonexistent')); // false
console.log(str.includes('To be', 1)); // false
console.log(str.includes('TO BE')); // false
```

### indexOf

- String 객체에서 주어진 값과 일치하는 첫번째 인덱스를 반환한다.

```javascript
const paragraph = 'The quick brown fox jumps over the lazy dog. If the dog barked, was it really lazy?';
const searchTerm = 'dog';
const indexOfFirst = paragraph.indexOf(searchTerm);
console.log(`The index of the first "${searchTerm}" from the beginning is ${indexOfFirst}`);
// expected output: "The index of the first "dog" from the beginning is 40"
console.log(`The index of the 2nd "${searchTerm}" is ${paragraph.indexOf(searchTerm, indexOfFirst + 1)}`);
// expected output: "The index of the 2nd "dog" is 52"
```

### lastIndexOf

- 일치하는 부분을 fromIndex로부터 역순으로 탐색하여 최초로 마주치는 인덱스를 반환한다.

```javascript
const paragraph = 'The quick brown fox jumps over the lazy dog. If the dog barked, was it really lazy?';
const searchTerm = 'dog';
console.log(`The index of the first "${searchTerm}" from the end is ${paragraph.lastIndexOf(searchTerm)}`);
// expected output: "The index of the first "dog" from the end is 52"
```

## 문자열 탐색 (정규식)

### match

- 문자열이 정규식과 매치되는 부분을 검색한다.

```javascript
var str = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
var regexp = /[A-E]/gi;
var matches_array = str.match(regexp);
console.log(matches_array);
// ['A', 'B', 'C', 'D', 'E', 'a', 'b', 'c', 'd', 'e']
```

- 정규식이 아닌 객체를 매개변수로 사용할 수 있다.

```javascript
var str1 = 'NaN means not a number. Infinity contains -Infinity and +Infinity in JavaScript.',
  str2 = 'My grandfather is 65 years old and My grandmother is 63 years old.',
  str3 = 'The contract was declared null and void.';
str1.match('number'); // "number"는 문자열임. ["number"]를 반환함.
str1.match(NaN); // NaN 타입은 숫자형임. ["NaN"]을 반환함.
str1.match(Infinity); // Infinity 타입은 숫자형임. ["Infinity"]를 반환함.
str1.match(+Infinity); // ["Infinity"]를 반환함.
str1.match(-Infinity); // ["-Infinity"]를 반환함.
str2.match(65); // ["65"]를 반환함
str2.match(+65); // 플러스 기호가 붙은 숫자형. ["65"]를 반환함.
str3.match(null); // ["null"]을 반환함.
```

### matchAll

```javascript
const regexp = /t(e)(st(\d?))/g;
const str = 'test1test2';
const array = [...str.matchAll(regexp)];
console.log(array[0]);
// expected output: Array ["test1", "e", "st1", "1"]
console.log(array[1]);
// expected output: Array ["test2", "e", "st2", "2"]
```

### search

- 정규 표현식과 String 객체간의 같은 것을 찾는다.
- 첫번째로 매치되는 것의 인덱스를 반환한다. (없다면 -1)

```javascript
const paragraph = 'The quick brown fox jumps over the lazy dog. If the dog barked, was it really lazy?';
// any character that is not a word character or whitespace
const regex = /[^\w\s]/g;
console.log(paragraph.search(regex));
// expected output: 43
console.log(paragraph[paragraph.search(regex)]);
// expected output: "."
```

## 문자열 채우기

### padStart

- 현재 문자열에 다른 문자열을 채워 주어진 길이를 만족하는 새로운 문자열을 반환한다.
- 채워넣기는 처음부터 적용된다.

```javascript
const str1 = '5';
console.log(str1.padStart(2, '0'));
// expected output: "05"
const fullNumber = '2034399002125581';
const last4Digits = fullNumber.slice(-4);
const maskedNumber = last4Digits.padStart(fullNumber.length, '*');
console.log(maskedNumber);
// expected output: "************5581"
'abc'.padStart(10); // "       abc"
'abc'.padStart(10, 'foo'); // "foofoofabc"
'abc'.padStart(6, '123465'); // "123abc"
'abc'.padStart(8, '0'); // "00000abc"
'abc'.padStart(1); // "abc"
```

### padEnd

- 현재 문자열에 다른 문자열을 채워 주어진 길이를 만족하는 새로운 문자열을 반환한다.
- 채워넣기는 끝부터 적용된다.

```javascript
const str1 = 'Breaded Mushrooms';
console.log(str1.padEnd(25, '.'));
// expected output: "Breaded Mushrooms........"
const str2 = '200';
console.log(str2.padEnd(5));
// expected output: "200  "
'abc'.padEnd(10); // "abc       "
'abc'.padEnd(10, 'foo'); // "abcfoofoof"
'abc'.padEnd(6, '123456'); // "abc123"
'abc'.padEnd(1); // "abc"
```

### repeat

- 문자열을 주어진 횟수만큼 반복해 붙인 새로운 문자열을 반환한다.

```javascript
'abc'.repeat(-1); // RangeError
'abc'.repeat(0); // ''
'abc'.repeat(1); // 'abc'
'abc'.repeat(2); // 'abcabc'
'abc'.repeat(3.5); // 'abcabcabc' (count will be converted to integer)
'abc'.repeat(1 / 0); // RangeError
({ toString: () => 'abc', repeat: String.prototype.repeat }.repeat(2));
// 'abcabc' (repeat() is a generic method)
```

### trim

- 문자열 양 끝 공백을 제거한다.
- 공백이란 모든 공백문자(space, tab, NBSP 등)와 모든 개행문자(LF, CR 등)를 의미한다.

```javascript
const greeting = '   Hello world!   ';
console.log(greeting);
// expected output: "   Hello world!   ";

console.log(greeting.trim());
// expected output: "Hello world!";
```

### trimStart

- 문자열 시작 부분의 공백을 제거한다.
- trimLeft라는 별칭으로 호출 가능하다.

```javascript
const greeting = '   Hello world!   ';
console.log(greeting);
// expected output: "   Hello world!   ";

console.log(greeting.trimStart());
// expected output: "Hello world!   ";
```

### trimEnd

- 문자열 끝 부분의 공백을 제거한다.
- trimRight라는 별칭으로 호출 가능하다.

```javascript
const greeting = '   Hello world!   ';
console.log(greeting);
// expected output: "   Hello world!   ";

console.log(greeting.trimEnd());
// expected output: "   Hello world!";
```

## 문자열 일부분 변경

### replace

- 어떤 패턴에 일치하는 일부 또는 모든 부분이 교체된 새로운 문자열을 반환한다.
- 패턴이 문자열인 경우에는 첫번째 문자열만 치환된다.

```javascript
const p = 'The quick brown fox jumps over the lazy dog. If the dog reacted, was it really lazy?';
console.log(p.replace('dog', 'monkey'));
// expected output: "The quick brown fox jumps over the lazy monkey. If the dog reacted, was it really lazy?"
const regex = /Dog/i;
console.log(p.replace(regex, 'ferret'));
// expected output: "The quick brown fox jumps over the lazy ferret. If the dog reacted, was it really lazy?"
```

### replaceAll

```javascript
const p = 'The quick brown fox jumps over the lazy dog. If the dog reacted, was it really lazy?';
console.log(p.replaceAll('dog', 'monkey'));
// expected output: "The quick brown fox jumps over the lazy monkey. If the monkey reacted, was it really lazy?"
// global flag required when calling replaceAll with regex
const regex = /Dog/gi;
console.log(p.replaceAll(regex, 'ferret'));
// expected output: "The quick brown fox jumps over the lazy ferret. If the ferret reacted, was it really lazy?"
```

## 문자열 자르기

### slice

- 문자열의 일부를 추출하면서 새로운 문자열을 반환한다.

```javascript
const str = 'The quick brown fox jumps over the lazy dog.';
console.log(str.slice(31));
// expected output: "the lazy dog."
console.log(str.slice(4, 19));
// expected output: "quick brown fox"
console.log(str.slice(-4));
// expected output: "dog."
console.log(str.slice(-9, -5));
// expected output: "lazy"
```

```javascript
var str1 = 'The morning is upon us.', // the length of str1 is 23.
  str2 = str1.slice(1, 8),
  str3 = str1.slice(4, -2),
  str4 = str1.slice(12),
  str5 = str1.slice(30);
console.log(str2); // OUTPUT: he morn
console.log(str3); // OUTPUT: morning is upon u
console.log(str4); // OUTPUT: is upon us.
console.log(str5); // OUTPUT: ""
```

### split

- 문자열을 구분자를 이용해서 여러개의 문자열로 나눈다.

```javascript
const str = 'The quick brown fox jumps over the lazy dog.';
const words = str.split(' ');
console.log(words[3]);
// expected output: "fox"
const chars = str.split('');
console.log(chars[8]);
// expected output: "k"
const strCopy = str.split();
console.log(strCopy);
// expected output: Array ["The quick brown fox jumps over the lazy dog."]
```

## 대소문자 변경

### toLowerCase

- 문자열을 소문자로 반환한다.

```javascript
const sentence = 'The quick brown fox jumps over the lazy dog.';
console.log(sentence.toLowerCase());
// expected output: "the quick brown fox jumps over the lazy dog."
```

### toUpperCase

- 문자열을 대문자로 반환한다.

```javascript
const sentence = 'The quick brown fox jumps over the lazy dog.';
console.log(sentence.toUpperCase());
// expected output: "THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG."
```
