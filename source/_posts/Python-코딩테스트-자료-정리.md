---
title: Python 코딩테스트 자료 정리
date: 2022-10-16 17:57:03
tags:
  - Python
categories:
  - Python
---

## 그리디 알고리즘

- 현재 상황에서 지금 당장 좋은 것만을 고르는 방법
- 그리디 알고리즘은 기준에 따라 좋은 것을 선택하는 알고리즘이므로 문제에서 '가장 큰 순서대로', '가장 작은 순서대로'와 같은 기준을 제시해준다.

## 구현 문제

- 구현 문제는 머릿속에 있는 알고리즘을 소스코드로 바꾸는 유형
- 완전 탐색 문제는 모든 경우의 수를 전부 계산하는 해결 방법
- 시뮬레이션은 문제에서 제시한 알고리즘을 한 단계씩 차례대로 직접 수행해야 하는 방법

### 완전 탐색 문제

- 완전 탐색 알고리즘은 가능한 경우의 수를 모두 검사하는 탐색
- 비효율적인 시간 복잡도를 가지고 있으므로 데이터 개수가 큰 경우에 정상적으로 작동하지 않을수도 있다.
- 일반적으로 확일할 전체 데이터가 100만개 이하일 때 완전 탐색을 이용한다.

### 시뮬레이션 이동 문제

- 일반적으로 방향을 설정해서 이동하는 문제 유형에서는 dx, dy라는 별도의 리스트를 만들어 방향을 정하는 것이 좋다.
- 현재 캐릭터가 북쪽으로 이동하기 위해서는 x, y 좌표를 각각 dx[i], dy[i] 만큼 더한다.
- 반복문을 이용하여 모든 방향을 차례대로 이동할 수 있다는 점에서 유용하다.

```python
## 상하좌우

N = int(input())
A = input().split()

# L, R, U, D
dx = [0, 0, -1, 1]
dy = [-1, 1, 0, 0]
move_type = ['L', 'R', 'U', 'D']

x, y = 1, 1

for plan in A:
  for i in range(len(move_type)):
    if move_type[i] == plan:
      temp_x = x + dx[i]
      temp_y = y + dy[i]

      if temp_x < 1 or temp_x > N or temp_y < 1 or temp_y > N:
        continue

      x = temp_x
      y = temp_y

print(x, y)

"""
5
R R R U D D

3 4
"""
```

## DFS, BFS

### 그래프

- 인접 행렬: 2차원 배열로 그래프의 연결 관계르 표현하는 방법 -> 연결이 되지 않는 노드끼리는 무한의 비용으로 작성한다. (논리적으로 가질 수 없는 큰 값)
- 인접 리스트: 리스트로 그래프의 연결 관계를 표현하는 방법

### Stack

```python
stack = []

stack.append(1)
stack.append(2)
stack.append(3)
stack.append(4)
stack.append(5)

stack.pop()

stack.append(6)
stack.append(7)

stack.pop()

print(stack)
print(stack[::-1])
```

### Queue

```python
from collections import deque

queue = deque()

queue.append(1)
queue.append(2)
queue.append(3)
queue.append(4)
queue.append(5)

queue.popleft()

queue.append(6)
queue.append(7)

queue.popleft()

print(queue)
queue.reverse()
print(queue)
```

### DFS

- DFS는 스택 자료구조를 이용한다.
  1. 탐색 시작 노드를 스택에 삽입하고 방문 처리를 한다.
  2. 스택의 최상단 노드에 방문하지 않은 인접 노드가 있다면 그 인접 노드를 스택에 넣고 방문 처리를 한다. 방문하지 않은 인접 노드가 없다면 스택에서 최상단 노드를 꺼낸다.
  3. 2번의 과정을 더 이상 수행할 수 없을때까지 한다.

```python
def dfs(graph, v, visited):
  visited[v] = True

  print(v, end=' ')

  for i in graph[v]:
    if not visited[i]:
      dfs(graph, i, visited)


graph = [
  [],
  [2,3,8],
  [1,7],
  [1,4,5],
  [3,5],
  [3,4],
  [7],
  [2,6,8],
  [1,7],
]

visited = [False] * 9

dfs(graph, 1, visited)
```

### BFS

- BFS는 큐 자료구조를 이용한다.
  1. 탐색 시작 노드를 큐에 삽입하고 방문 처리를 한다.
  2. 큐에서 노드를 꺼내 해당 노드의 인접 노드 중에서 바움하지 않은 노드를 모두 큐에 삽입하고 방문 처리를 한다.
  3. 2번의 과정을 더 이상 수행할 수 없을때까지 한다.
- 최단거리를 구하는 것은 BFS를 이용하는 것이 유리하다.

```python
from collections import deque

def bfs(graph, start, visited):
  queue = deque([start])

  visited[start] = True

  while queue:
    v = queue.popleft()
    print(v, end=' ')

    for i in graph[v]:
      if not visited[i]:
        queue.append(i)
        visited[i] = True

graph = [
  [],
  [2,3,8],
  [1,7],
  [1,4,5],
  [3,5],
  [3,4],
  [7],
  [2,6,8],
  [1,7],
]

visited = [False] * 9

bfs(graph, 1, visited)
```

## 정렬

### sorted()

- 리스트나 딕셔너리 자료형 등을 입력받아서 정렬된 결과를 출력한다.
- 집합이나 딕셔너리 자료형을 입력하여도 반환되는 결과는 리스트이다.

```python
result = sorted(array)
```

### sort()

- 리스트 객체이 내장 함수인 sort()를 사용하면, 별도의 정렬된 리스트가 반환되지 않고, 내부 원소가 바료 정렬된다.

```python
array.sort()
```

### Key 매개변수

- sorted()나 sort()를 이용할 경우에는 key 매개변수를 입력으로 받을 수 있다.
- key 값으로는 하나의 함수가 들어가야 하며, 정렬 기준이 된다.

```python
array = [('바나나', 2), ('사과', 5), ('당근', 3)]

def setting(data):
  return data[1]

result = sorted(array, key=setting)
print(array)
```

### 퀵 정렬

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

def quick_sort(array, start, end):
  if start >= end:
    return

  pivot = start
  left = start + 1
  right = end

  while left <= right:
    while left <= end and array[left] <= array[pivot]:
      left += 1

    while right > start and array[right] >= array[pivot]:
      right -= 1

    if left > right:
      array[right], array[pivot] = array[pivot], array[right]
    else:
      array[left], array[right] = array[right], array[left]

  quick_sort(array, start, right - 1)
  quick_sort(array, right + 1, end)

quick_sort(array, 0, len(array) - 1)
print(array)
```

#### Python 문법을 사용한 퀵 정렬

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

def quick_sort(array):
  if len(array) <= 1:
    return array

  pivot = array[0]
  tail = array[1:]

  left_side = [x for x in tail if x <= pivot]
  right_side = [x for x in tail if x > pivot]

  return quick_sort(left_side) + [pivot] + quick_sort(right_side)

print(quick_sort(array))
```

### 계수 정렬

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 9, 1, 4, 8, 0, 5, 2]

count = [0] * (max(array) + 1)

for i in range(len(array)):
  count[array[i]] += 1

for i in range(len(count)):
  for j in range(count[i]):
    print(i, end=' ')
```

## 이진 탐색

```python
def binary_search(array, target, start, end):
  while start <= end:
    mid = (start + end) // 2

    if array[mid] == target:
      return mid
    elif array[mid] > target:
      end = mid - 1
    else:
      start = mid + 1

  return None

array = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
target = 7

print(binary_search(array, target, 0, len(array) - 1))
```

### 파라메트릭 서치

- 파라메트릭 서치는 최적화 문제를 결정 문제로 바꾸어 해결하는 기법이다.
- 원하는 조건을 만족하는 가장 알맞은 값을 찾는 문제에 주로 파라메트릭 서치를 이용한다.
- 파라메트릭 서치에서 이진 탐색을 구현해야 하는 경우에는 재귀적으로 구현하지 않고, 반복문을 이용해 구현하는 것이 더 간결하다.

```python
## 떡볶이 떡 만들기

n, m = list(map(int, input().split(' ')))
array = list(map(int, input().split()))

start = 0
end = max(array)

result = 0

while start <= end:
  total = 0
  mid = (start + end) // 2

  for x in array:
    if x > mid:
      total += x - mid
  if total < m:
    end = mid - 1
  else:
    result = mid
    start = mid + 1

print(result)

"""
4 6
19 15 10 17

15
"""
```

## 다이나믹 프로그래밍

- 어떠한 문제는 메모리 공간을 약간 더 사용함으로써, 연산 속도를 비약적으로 증가시킬 수 있다. 대표적인 방법이 다이나믹 프로그래밍이다.
- 다이나믹 프로그래밍 사용 조건
  1. 큰 문제를 작은 문제로 나눌 수 있다.
  2. 작은 문제에서 구한 정답은 그것을 포함하는 큰 문제에서도 동일하다.

### 메모이제이션 (Memoization)

- 메모이제이션은 다이나밋 프로그래밍을 구현하는 방법 중 한 종류로, 한 번 구한 결과를 메모리 공간에 메모해두고 같은 식을 다시 호출하면 메모한 결과를 그대로 가져오는 기법이다.
- 캐싱이라고도 한다.
- 재귀함수 대신에 반복문을 사용하여 오버헤드를 줄일 수 있다.
- 일반적으로 반복문을 이용한 다이나믹 프로그래밍이 더 성능이 좋기 때문이다.
- 재귀 함수를 이용하여 다이나믹 프로그래밍 소스코드를 작성하는 방법을, 큰 문제를 해결하기 위해 작은 문제를 호출한다고 하여 탑 다운 방식이라고 한다.
- 반복문을 이용하여 소스코드를 작성하는 경우 작은 문제부터 차근차근 답을 도출한다고 하여 보텀 업 방식이라고 한다.
- 보텀 업 방식에서 사용되는 결과 저장용 리스트는 'DP 테이블'이라고 한다.

#### 메모이제이션

```python
d = [0] * 100

def fibo(x):
  if x == 1 or x == 2:
    return 1

  if d[x] != 0:
    return d[x]

  d[x] = fibo(x - 2) + fibo(x - 1)
  return d[x]

print(fibo(99))
```

#### DP 테이블

```python
d = [0] * 100

d[1] = 1
d[2] = 1
n = 99

for i in range(3, n + 1):
  d[i] = d[i - 2] + d[i - 1]

print(d[n])
```

## 최단거리 알고리즘

### 다익스트라 최단 경로 알고리즘

- 다익스트라 알고리즘은 기본적으로 그리디 알고리즘으로 분류한다.
- 매번 가장 비용이 적은 노드를 선택해서 임의의 과정을 반복하기 때문이다.
  1. 출발 노드를 설정한다.
  2. 최단 거리 테이블을 초기화한다.
  3. 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택한다.
  4. 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신한다.
  5. 3, 4를 반복한다.
- 각 노드에 대한 현재까지의 최단 거리 정보를 항상 1차원 리스트에 저장하며 리스트를 계속 갱신한다는 특징이 있다.
- 다익스트라 알고리즘이 진행되면서 한 단계당 하나의 노드에 대한 최단 거리를 확실히 찾는 것으로 이해할 수 있다.
- 인접 리스트를 이용한다.

```python
import sys
input = sys.stdin.readline
INF = int(1e9)

n = 6 # 노드의 개수
m = 11  # 간선의 개수
start = 1 # 시작 노드

graph = [[] for i in range(n + 1)] # 노드 정보
visited = [False] * (n + 1) # 방문 여부
distance = [INF] * (n + 1) # 최단거리

graph[1].append((2, 2))
graph[1].append((3, 5))
graph[1].append((4, 1))
graph[2].append((3, 3))
graph[2].append((4, 2))
graph[3].append((2, 3))
graph[3].append((6, 5))
graph[4].append((3, 3))
graph[4].append((5, 1))
graph[5].append((3, 1))
graph[5].append((6, 2))

def get_smallest_node():
  min_value = INF
  index = 0

  for i in range(1, n + 1):
    if distance[i] < min_value and not visited[i]:
      min_value = distance[i]
      index = i

  return index

def dijkstra(start):
  distance[start] = 0
  visited[start] = True

  for j in graph[start]:
    distance[j[0]] = j[1]

  for i in range(n - 1):
    now = get_smallest_node()
    visited[now] = True

    for j in graph[now]:
      cost = distance[now] + j[1]

      if cost < distance[j[0]]:
        distance[j[0]] = cost

dijkstra(start)

for i in range(1, n + 1):
  if distance[i] == INF:
    print('INFINITY')
  else:
    print(distance[i])
```

#### 개선된 다익스트라 알고리즘

- 힙 자료구조를 이용한다.
- 힙 자료구조는 우선순위 큐를 구현하기 위하여 서용하는 자료구조 중 하나이다.
- 비용이 적은 노드를 우선하여 방문하므로 최소 힙 구조를 기반으로 하는 파이썬 우선순위 큐 라이브러리를 이용한다.
- 만약, 최소 힙을 최대 힙처럼 사용하기 위해서는 일부러 우선순위에 해당하는 값에 음수 부호를 붙여서 넣었다가 나중에 꺼낸 다음 다시 음수 부호를 붙여서 원래의 값으로 돌리는 방식을 사용할 수 있다.

```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9)

n = 6 # 노드의 개수
m = 11  # 간선의 개수
start = 1 # 시작 노드

graph = [[] for i in range(n + 1)] # 노드 정보
distance = [INF] * (n + 1) # 최단거리

graph[1].append((2, 2))
graph[1].append((3, 5))
graph[1].append((4, 1))
graph[2].append((3, 3))
graph[2].append((4, 2))
graph[3].append((2, 3))
graph[3].append((6, 5))
graph[4].append((3, 3))
graph[4].append((5, 1))
graph[5].append((3, 1))
graph[5].append((6, 2))

def dijkstra(start):
  q = []
  heapq.heappush(q, (0, start))
  distance[start] = 0

  while q:
    dist, now = heapq.heappop(q)

    if distance[now] < dist:
      continue

    for i in graph[now]:
      cost  = dist + i[1]
      if cost < distance[i[0]]:
        distance[i[0]] = cost
        heapq.heappush(q, (cost, i[0]))

dijkstra(start)

for i in range(1, n + 1):
  if distance[i] == INF:
    print('INFINITY')
  else:
    print(distance[i])
```

### 플로이들 워셜 알고리즘

- 다익스트라 알고리즘은 한 지점에서 다른 특정 지점까지의 최단 경로를 구해야 하는 경우에 사용할 수 있는 최단 거리 알고리즘이다.
- 플로이드 워셜 알고리즘은 모든 지점에서 다른 모든 지점까지의 최단 경로를 모두 구해야 하는 경우에 사용할 수 있는 최단 거리 알고리즘이다.
- 플로이드 워셜 알고리즘은 단계마다 거쳐가는 노드를 기준으로 알고리즘을 수행한다.
- 2차원 리스트에 최단 거리 정보를 저장한다.
- 다이나믹 프로그래밍이다. (점화식에 맞게 2차원 리스트를 갱신한다.)
- 각 단계에서는 해당 노드를 거쳐 가능 경우를 고려한다. 예를 들어 1번 노드에 대해서 확인할 때는 1번 노드를 중간에 거쳐 가는 모든 경우를 고려한다. A -> 1번 노드 -> B로 가는 비용을 확인한 후 최단 거리를 갱신한다.
- 인접 행렬을 이용한다.

```python
INF = int(1e9)

n = 4 # 노드 개수
m = 7 # 간선 개수
graph = [[INF] * (n + 1) for _ in range(n + 1)]

for a in range(1, n + 1):
  for b in range(1, n + 1):
    if a == b:
      graph[a][b] = 0

graph[1][2] = 4
graph[1][4] = 6
graph[2][1] = 3
graph[2][3] = 7
graph[3][1] = 5
graph[3][4] = 4
graph[4][3] = 2

for k in range(1, n + 1):
  for a in range(1, n + 1):
    for b in range(1, n + 1):
      graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

for a in range(1, n + 1):
  for b in range(1, n + 1):
    if graph[a][b] == INF:
      print("INFINITY", end=' ')
    else:
      print(graph[a][b], end=' ')

  print()
```

## 그래프

- 그래프란 노드와 노드 사이에 연결된 간선의 정보를 가지고 있는 자료구조이다.
- 서로 다른 개체가 연결되었다는 이야기를 들으면 그래프를 떠올려야 한다.

### 서로소 집합

- 공통 원소가 없는 두 집합
- 서로소 집합 구조란 서로소 부분 집합들로 나누어진 원소들의 데이터를 처리하기 위한 자료구조이다.
- 서로소 집합 구조는 union과 find 2개의 연산으로 조작할 수 있다.
- union은 2개의 원소가 포함된 집합을 하나의 집합으로 합치는 연산이다.
- find는 특정한 원소가 속한 집합이 어떤 집합인지 알려주는 연산이다.
- 두 집합이 서로소 관계인지 확인할 수 있다는 말은 각 집합이 어떤 원소를 공통으로 가지고 있는지를 확인할 수 있다는 말과 같다.
- 트리 자료구조를 이용하여 표햔한다.
  1. union 연산을 확인하여 서로 연결된 두 노드 A, B를 확인한다.
  2. 모든 union 연산을 처리할 때까지 1번 과정을 반복한다.
- union 연산은 간선으로 표현한다.
- union 연산을 확인하면서 서로 다른 두 원소에 대해 합집합을 수행할 경우에는 각각이 루트 노드를 찾아서 더 큰 루트 노드가 더 작은 루트 노드 노드를 가리키도록 하면 된다.

```python
def find_parent(parent, x):
  if parent[x] != x:
    parent[x] = find_parent(parent, parent[x])
  return parent[x]

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
  a = find_parent(parent, a)
  b = find_parent(parent, b)

  if a < b:
    parent[b] = a
  else:
    parent[a] = b

v = 6 # 노드 개수
e = 4 # 간선 개수(union 연산)
parent = [0] * (v + 1) # 부모 테이블

# 부모 테이블에서 부모를 자기 자신을 초기화
for i in range(1, v + 1):
  parent[i] = i

union_parent(parent, 1, 4)
union_parent(parent, 2, 3)
union_parent(parent, 2, 4)
union_parent(parent, 5, 6)

print('각 원소가 속한 집합: ', end=' ')
for i in range(1, v + 1):
  print(find_parent(parent, i), end=' ')

print()

print('부모 테이블: ', end=' ')
for i in range(1, v + 1):
  print(parent[i], end=' ')
```

#### 서로소 집합을 이용한 사이클 판별

- 서로소 집합은 무방향 그래프 내에서의 사이클을 판별할 때 사용할 수 있다. (방향 그래프에서의 사이클 여부는 DFS를 이용하여 판별할 수 있다.)
- union 연산은 그래프에서의 간선으로 표현될 수 있다. 따라서, 간선을 하나씩 확인하면서 두 노드가 포함되어 있는 집합을 합치는 과정을 반복하는 것으로도 사이클을 판별할 수 있다.

1. 각 간선을 확인하며 두 노드의 루트 노드를 확인한다.
   - 루트 노드가 서로 다르다면 두 노드에 대해서 union 연산을 수행한다.
   - 루트 노드가 서로 같다면 사이클이 발생한 것이다.
2. 그래프에 포함되어 있는 모든 간선에 대해서 1번 과정을 반복한다.

```python
def find_parent(parent, x):
  if parent[x] != x:
    parent[x] = find_parent(parent, parent[x])
  return parent[x]

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
  a = find_parent(parent, a)
  b = find_parent(parent, b)

  if a < b:
    parent[b] = a
  else:
    parent[a] = b

v = 3
e = 3
parent = [0] * (v + 1)

for i in range(1, v + 1):
  parent[i] = i

cycle = False

for i in range(e):
  a, b = map(int , input().split())

  # 사이클이 발생한 경우 종료
  if find_parent(parent, a) == find_parent(parent, b):
    cycle = True
    break
  else:
    union_parent(parent, a, b)

if cycle:
  print('사이클이 발생했습니다.')
else:
  print('사이클이 발생하지 않았습니다.')

"""
1 2
1 3
2 3
"""
```

### 신장 트리

- 신장 트리란 하나의 그래프가 있을 때 모든 노드를 포함하면서 사이클이 존재하지 않는 부분 그래프이다.

#### 크루스칼 알고리즘 (Kruskal Algorithm)

- 최소한의 비용으로 신장 트리를 찾아야 하는 경우가 있다.
- 모든 간선에 대하여 정렬을 수행한 뒤에 가장 거리가 짧은 간선부터 집합에 포함시킨다.
- 이때, 사이클이 발생할 수 있는 간선의 경우 집합에 포함시키지 않는다.

1. 간선 데이터를 비용에 따라 오름차순으로 정렬한다.
2. 간선을 하나씩 확인하며 현재의 간선이 사이클을 발생시키는 지 확인한다.
   - 사이클이 발생하지 않는 경우 최소 신장 트리에 포함한다.
   - 사이클이 발생하는 경우 최소 신장 트리에 포함하지 않는다.
3. 모든 간선에 대해 2번 과정을 반복한다.

```python
def find_parent(parent, x):
  if parent[x] != x:
    parent[x] = find_parent(parent, parent[x])
  return parent[x]

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
  a = find_parent(parent, a)
  b = find_parent(parent, b)

  if a < b:
    parent[b] = a
  else:
    parent[a] = b

v = 7
e = 9
parent = [0] * (v + 1)

edges = [] # 모든 간선을 담을 리스트
result = 0 # 최종 비용을 담을 변수

for i in range(1, v + 1):
  parent[i] = i

edges.append((29, 1, 2))
edges.append((75, 1, 5))
edges.append((35, 2, 3))
edges.append((34, 2, 6))
edges.append((7, 3, 4))
edges.append((23, 4, 6))
edges.append((13, 4, 7))
edges.append((53, 5, 6))
edges.append((25, 6, 7))

edges.sort()

for edge in edges:
  cost, a, b = edge

  if find_parent(parent, a) != find_parent(parent, b):
    union_parent(parent, a, b)
    result += cost

print(result)
```

### 위상 정렬 (Topology Sort)

- 위상 정렬은 순서가 정해져 있는 일련의 작업을 차례대로 수행해야 할 때 사용할 수 있는 알고리즘이다.
- 위상 정렬이란 방향 그래프의 모든 노드를 방향성에 거스르지 않도록 순서대로 나열하는 것이다.

1. 진입 차수가 0인 노드를 큐에 넣는다.
2. 큐가 빌 때까지 다음의 과정을 반복한다.
   1. 큐에서 원소를 꺼내 해당 노드에서 출발하는 간선을 그래프에서 제거한다.
   2. 새롭게 진입 차수가 0이 된 노드를 큐에 넣는다.

- 모든 원소를 방문하기 전에 큐가 빈다면 사이클이 존재한다고 판단할 수 있다.
- 다시 말해,큐에서 원소가 V번 추출되기 전에 큐가 비어버리면 사이클이 발생한 것이다.
- 기본적읋 위상 정렬 문제에서는 사이클이 발생하지 않는다고 명시하는 경우가 많다.
- 과정을 수행하는 동안 큐에서 빠져나간 노드를 순서대로 출력하면 그것이 바로 위상 정렬을 수행한 결과이다.

```python
from collections import deque

v = 7
e = 8
indegree = [0] * (v + 1) # 모든 노드에 대한 진입차수는 0으로 초기화한다.
graph = [[] for i in range(v + 1)]  # 각 노드에 연결된 간선 정보를 담기 위한 연결 리스트 초기화

graph[1].append(2)
indegree[2] += 1
graph[1].append(5)
indegree[5] += 1
graph[2].append(3)
indegree[3] += 1
graph[2].append(6)
indegree[6] += 1
graph[3].append(4)
indegree[4] += 1
graph[4].append(7)
indegree[7] += 1
graph[5].append(6)
indegree[6] += 1
graph[6].append(4)
indegree[4] += 1

def topology_sort():
  result = [] # 알고리즘 수행 결과를 담을 리스트
  q = deque() # 큐 기능을 위한 deque 라이브러리 사용

  for i in range(1, v + 1):
    if indegree[i] == 0:
      q.append(i)

  while q:
    now = q.popleft()
    result.append(now)

    for i in graph[now]:
      indegree[i] -= 1

      if indegree[i] == 0:
        q.append(i)

  for i in result:
    print(i, end=' ')

topology_sort()
```
