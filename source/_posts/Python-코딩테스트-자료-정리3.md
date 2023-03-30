---
title: Python 코딩테스트 자료 정리3
date: 2023-03-30 13:17:35
tags:
  - Python
categories:
  - Python
---

## input()

- https://kihyeon-hong.github.io/2022/09/05/Python-%EA%B8%B0%EB%B0%98%EC%9D%98-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%9E%85%EB%A0%A5-%EC%A0%95%EB%A6%AC/

## deque

```python
from collections import deque

queue = deque([1, 2, 3])
queue.append(4)
queue.append(5)

print(queue)    # deque([1, 2, 3, 4, 5])

print(queue.popleft())  # 1
print(queue.popleft())  # 2
print(queue.popleft())  # 3

print(list(queue))  # [4, 5]
```

## defaultdict

```python
from collections import defaultdict

dic = defaultdict(int)  # str, list, set...

for _ in range(10):
    dic['A'] += 1
    dic['B'] += 2

print(dic)  # defaultdict(<class 'int'>, {'A': 10, 'B': 20})
print(list(dic))    # ['A', 'B']
print(dic.keys())   # dict_keys(['A', 'B'])
```

## heap

```python
from heapq import heapify, heappush, heappop

heap = [5, 6, 1, 2, 8]

heapify(heap)

a = heappop(heap)
b = heappop(heap)

print(a)    # 1
print(b)    # 2

heappush(heap, a + b)

print(heap) # [3, 5, 8, 6]
```

## set

```python
s = set([1, 1, 1, 1, 1, 1, 2, 3])

s.add(4)
s.add(5)

s.update([6, 7, 8, 9, 10])

print(s)    # {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
print(list(s))  # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

s.remove(1)
s.remove(2)
s.remove(3)

print(s)    # {4, 5, 6, 7, 8, 9, 10}
```

## 순열과 조합

```python
from itertools import combinations, permutations

array = [1, 2, 3, 4]

for p in permutations(array, 2):    # 순열
    print(p)

'''
(1, 2)
(1, 3)
(1, 4)
(2, 1)
(2, 3)
(2, 4)
(3, 1)
(3, 2)
(3, 4)
(4, 1)
(4, 2)
(4, 3)
'''

for c in combinations(array, 2):    # 조합
    print(c)

'''
(1, 2)
(1, 3)
(1, 4)
(2, 3)
(2, 4)
(3, 4)
'''
```

## 정렬

```python
array1 = [5, 3, 7, 2, 9, 1, 4, 6, 8]
array2 = sorted(array1)

print(array1)   # [5, 3, 7, 2, 9, 1, 4, 6, 8]
print(array2)   # [1, 2, 3, 4, 5, 6, 7, 8, 9]

array1.sort()

print(array1)   # [1, 2, 3, 4, 5, 6, 7, 8, 9]

array1.reverse()

print(array1)   # [9, 8, 7, 6, 5, 4, 3, 2, 1]
```

## 람다식(lambda)

```python
array = [(2, 1), (1, 1), (1, 2), (4, 1), (1, 3), (2, 3), (3, 3), (2, 2), (3, 2), (3, 1)]
array.sort(key=lambda x: (x[0], -x[1]), reverse=False)

print(array)    # [(1, 3), (1, 2), (1, 1), (2, 3), (2, 2), (2, 1), (3, 3), (3, 2), (3, 1), (4, 1)]
```

## filter

```python
array = [1, 2, 3, 4, 5, 6, 7, 8, 9]

f = filter(lambda x: x >= 5, array)

print(f)    # <filter object at 0x000002011537AB30>
print(list(f))  # [5, 6, 7, 8, 9]
```

## math

```python
import math

# x에 y 승을 계산한 결괏값을 반환
print(math.pow(3, 2))   # 9.0

# 주어진 인자의 제곱근의 값을 반환
print(math.sqrt(25))    # 5.0

# 주어진 인자의 소수점을 올림하여 정수로 변환
print(math.ceil(3.14))  # 4

# 주어진 인자의 소숫점을 내림하여 정수로 변환 (무조건 내림 처리)
print(math.floor(3.78))  # 3

# 주어진 인자의 소숫점을 내림하여 정수로 변환 (0에 가깝게)
print(math.trunc(3.14))  # 3

# 두 번째 인자의 부호를 가져와 첫 번째 인자의 부호에 적용
print(math.copysign(3.14, -3))  # -3.14

# 절댓값을 반환
print(math.fabs(-3.14))  # 3.14

# 팩토리얼 함수
print(math.factorial(5))  # 120

# 입력 받은 인자의 값과 동일하게 연산 가능한 m * 2^e과 같은 값을 가지는 m, e를 반환 (0.78125*2**7 = 100)
print(math.frexp(100))  # (0.78125, 7)

# math.frexp()의 반대 함수로써, m * 2^e에 각각 대입, 계산한 값을 반환
print(math.ldexp(0.78125, 7))  # 100.0

# 두 수의 최대 공약수를 반환
print(math.gcd(6, 8))  # 2

# 입력값을 정수와 소수 부분으로 분리
print(math.modf(3.14))  # (0.14000000000000012, 3.0)

# 로그 함수이며 b를 밑으로 하는 log a에 대한 로그 값을 리턴
print(math.log(10, 10))  # 1.0
```

## 최대공약수, 최소공배수

```python
def gcd(a, b):
    while b > 0:
        a, b = b, a % b
    return a

def lcm(a, b):
    return a * b / gcd(a, b)


print('최대공약수', gcd(21, 28))    # 최대공약수 7
print('최소공배수', lcm(21, 28))    # 최소공배수 84.0
```

### 에라토스테네스의 체

```python
import math

def is_prime_number(n):
	arr = [True for _ in range(n + 1)]

	for i in range(2, int(math.sqrt(n)) + 1):
		if arr[i] == True:
			cnt = 2

		while i * cnt <= n:
			arr[i * cnt] = False
			cnt += 1

	return [i for i in range(2, n + 1) if arr[i]]

print(is_prime_number(100))
# [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97]
```
