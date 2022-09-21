---
title: Python 기반의 데이터 입력 정리
date: 2022-09-05 23:16:26
tags:
  - Python
categories:
  - Python
---

## 정수 입력받기

- 한줄의 문자열 데이터를 입력받아, 정수로 변환한다.

```python
N = int(input())
print(N)
```

- 입력

```bash
12345
```

- 출력

```bash
12345
```

## 여러 데이터 입력받기

- 공백으로 구분된 데이터를 입력받아, 공백을 기준으로 구분된 배열을 반환한다.
- 정수를 입력하여도 문자열로 저장된다.

```python
N = input().split()
print(N)
```

- 입력

```bash
1 2 3 4 5
```

- 출력

```bash
['1', '2', '3', '4', '5']
```

## 여러 데이터 입력받기(정수)

### Map 이용하기

- 나눌 요소의 개수만큼 변수(N, M)를 선언해줘야 한다.
- 만약, 요소의 개수가 일치하지 않는다면 오류가 발생한다.

```python
N, M = map(int, input().split())
print(N, M)
```

- 입력

```bash
10 20
```

- 출력

```bash
10 20
```

### list와 map 이용하기

- 요소의 개수를 모를 경우 list를 이용한다.

```python
arr = list(map(int, input().split()))
print(arr)
```

- 입력

```bash
10 20 30 40 50
```

- 출력

```bash
[10, 20, 30, 40, 50]
```

## 문자열 요소 나누기

- 한줄의 데이터(문자열이나 정수)를 입력받아, 각각의 요소로 나눈다.

```python
arr = list(input())
print(arr)
```

- 입력

```bash
abcdefg
```

- 출력

```bash
['a', 'b', 'c', 'd', 'e', 'f', 'g']
```

### 문자열 요소 나누기(정수)

```python
arr = list(map(int, input()))
print(arr)
```

- 입력

```bash
12345
```

- 출력

```bash
[1, 2, 3, 4, 5]
```

## 일정 횟수만큼 동작 반복하기

- 먼저, 반복횟수를 입력하고, 각각의 반복문 내에서 입력을 받은 후, 작업을 수행한다.

```python
for _ in range(int(input())):
  print(input())
```

- 입력

```bash
5
a
a
b
b
c
c
d
d
e
e
```

## 문자열을 문자로 분리하여 반복문 수행하기

- 문자열을 입력한 후, 문자열을 각각의 문자로 분리하여 반복문을 수행한다.

```python
for ch in input():
  print(ch)
```

- 입력

```bash
abcdefg
```

- 출력

```bash
a
b
c
d
e
f
g
```

## 일정 횟수만큼 데이터 입력하기

- 입력받을 횟수를 입력한 후, 입력 횟수만큼 입력을 받는다.

```python
N = int(input())
board = [input() for _ in range(N)]

print(board)
```

- 입력

```bash
5
a
b
c
d
e
```

- 출력

```bash
['a', 'b', 'c', 'd', 'e']
```

## 2차원 정수 배열 생성

- 행의 개수를 입력한 후, 각각 행의 요소를 입력한다.

```python
N = int(input())
arr = [list(map(int, input().split())) for _ in range(N)]

print(arr)
```

- 입력

```bash
3
1 2 3
4 5 6
7 8 9
```

- 출력

```bash
[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

## 2차원 정수 배열 생성하기2

- 입력받은 횟수를 기반으로 2차원 배열을 생성한다.

```python
N = int(input())
arr = [[i] * 3 for i in range(N)]

print(arr)
```

- 입력

```bash
3
```

- 출력

```bash
[[0, 0, 0], [1, 1, 1], [2, 2, 2]]
```

## 빠른 입출력

- input()보다 sys.stdin.readline()가 메모리와 시간을 적게 소요한다.

```python
import sys
input = sys.stdin.readline

x = input()
print(x)
```

- 입력

```bash
abcdefg
```

- 출력

```bash
abcdefg
```

### rstrip()

- 소스코드에 readline을 입력하면 입력 후 엔터가 줄바꿈 기호로 입력이 되는데, 이 공백 문자를 제거하는 용도로 사용한다.

```python
import sys
input = sys.stdin.readline().rstrip()

print(input)
```
