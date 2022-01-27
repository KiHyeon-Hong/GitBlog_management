---
title: Javascript 정규표현식 정리
date: 2022-01-27 10:26:35
tags:
  - javascript
categories:
  - Javascript
---

## 정규표현식이란?

- pattern과 flag를 이용한다.

```
/regex?/i
```

## 사용법

```
/Hi/gm
```

- Hi와 정확히 일치하는 것을 찾는다.

```
/Hi|Hello/gm
```

- Hi 또는 Hello와 정확히 일치하는 것을 찾는다.

```
/(Hi|Hello)/gm
```

- 소괄호를 통해 묶어주면, match도 되고, group1에 Hi가 지정된다.

```
/(Hi|Hello)|(to)/gm
```

- group1에는 Hi or Hello, group2에는 to와 일치하는 것을 찾으며, 없을 경우 undefined

```
/((Hi|Hello)|(to))/gm
```

- group1은 Hi, Hello, to를 찾으며, group2에는 Hi or Hello, group3에는 to와 일치하는 것을 찾으며, 없을 경우 undefined

```
/gr(e|a)y/
```

- grey, gray를 찾는다. 이러할 경우 e, a가 그룹으로 묶이는데, 만약 그룹으로 묶고 싶지 않다면 그룹 앞에 ?:을 붙인다.

```
/gr(?:e|a)y/
```

```
/gr[ae]y/
```

- /gr(e|a)y/와 동일하며, 찾고싶은 문자열 집합체를 작성한다.
- 하나라도 만족하는 것을 찾는다.

```
/gr[abcdef]y/
```

- /gr[a-f]y/와 동일하다

```
/gr[^a-f]y/
```

- a부터 f까지를 제외한 문자열을 찾는다.

## Quantifiers

```
/gra?y/
```

- ?는 없거나 있거나 이다. (gray, gry)

```
/gra*y/
```

- 없거나 있거나 많거나 이다. (gry, gray, graay, graaay)

```
/gra+y/
```

- 하나 있거나 많거나 이다. (gray, graay, graaay)

```
/gra{2}y/
```

- a가 2번 나오는 단어를 찾는다. (graay)

```
/gra{2,3}y/
```

- a가 2~3번 나오는 단어를 찾는다. (graay, graaay)

```
/gra{2,}y/
```

- a가 2번 이상 나오는 단어를 찾는다. (graay, graaay, graaaay)

## Boundary-type

```
/\bYa/
```

- \b를 앞에 사용하면 단어의 맨 앞에서 나오는 Ya만 매칭한다.

```
/Ya\b/
```

- \b를 뒤에 사용하면 단어의 맨 뒤에서 나오는 Ya만 매칭한다.

```
/\BYa/
```

- \b를 앞에 사용하면 단어의 맨 앞에서 나오는 Ya만 빼고 전부 매칭한다.

```
/Ya\B/
```

- \b를 뒤에 사용하면 단어의 맨 뒤에서 나오는 Ya만 빼고 전부 매칭한다.

```
/^Ya/
```

- ^는 문장에서 시작하는 Ya를 찾는다.

```
/Ya$/
```

- $는 문장에서 끝나는 Ya를 찾는다.
- 이때 플래그의 멀티라인을 작성하지 않으면, 문장 전체에서 시작하는 Ya와 문장 전체에서 끝나는 Ya를 찾기 때문에 아무 것도 선택되지 않을 수도 있다.

## Character classes

```
/./
```

- 줄바꿈 문자를 제외한 모든 문자열을 선택한다.
- 만약에 .를 진짜로 찾고 싶은것이라면, \를 이용해야 한다.

```
/\./
```

- 특수 문자인 경우에는 \ 다음에 작성을 해야된다.

```
/\d/
```

- 숫자를 전부 찾는다.

```
/\D/
```

- 숫자를 제외하고 전부 찾는다.

```
/\w/
```

- 문자를 전부 찾는다.

```
/\W/
```

- 문자를 제외하고 전부 찾는다.

```
/\s/
```

- 공백을 전부 찾는다.

```
/\S/
```

- 공백을 제외하고 전부 찾는다.

## 자바스크립트에서 사용 방법

```javascript
const regex = /\d/;
const s = 'abcdefg';

s.match(regex);
```
