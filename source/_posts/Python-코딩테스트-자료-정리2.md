---
title: Python 코딩테스트 자료 정리2
date: 2022-11-11 22:47:16
tags:
  - Python
categories:
  - Python
---

## Stack

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

```bash
[1, 2, 3, 4, 6]
[6, 4, 3, 2, 1]
```

## Queue

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

```bash
deque([3, 4, 5, 6, 7])
deque([7, 6, 5, 4, 3])
```

## DFS

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

```bash
1 2 7 6 8 3 4 5
```

## BFS

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

```bash
1 2 3 8 7 4 5 6
```

## Selection Sort

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(len(array)):
  min_index = i

  for j in range(i + 1, len(array)):
    if array[min_index] > array[j]:
      min_index = j

  array[i], array[min_index] = array[min_index], array[i]

print(array)
```

```bash
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## Insertion Sort

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(1, len(array)):
  for j in range(i, 0, -1):
    if array[j] < array[j - 1]:
      array[j], array[j - 1] = array[j - 1], array[j]
    else:
      break

print(array)
```

```bash
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## Quick Sort

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

```bash
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## Quick Sort(Python version)

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

```bash
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## Count Sort

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 9, 1, 4, 8, 0, 5, 2]

count = [0] * (max(array) + 1)

for i in range(len(array)):
  count[array[i]] += 1

for i in range(len(count)):
  for j in range(count[i]):
    print(i, end=' ')
```

```bash
0 0 1 1 2 2 3 4 5 5 6 7 8 9 9
```

## Binary Search

```python
def binary_search(array, target, start, end):
  if start > end:
    return None

  mid = (start + end) // 2

  if array[mid] == target:
    return mid
  elif array[mid] > target:
    return binary_search(array, target, start, mid - 1)
  else:
    return binary_search(array, target, mid + 1, end)


array = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
target = 7

print(binary_search(array, target, 0, len(array) - 1))
```

```bash
3
```

## Binary Search (재귀 X)

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

```bash
3
```

## Memoization

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

```bash
218922995834555169026
```

## DP Table

```python
d = [0] * 100

d[1] = 1
d[2] = 1
n = 99

for i in range(3, n + 1):
  d[i] = d[i - 2] + d[i - 1]

print(d[n])
```

```bash
218922995834555169026
```

## Dijkstra

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

```bash
0
2
3
1
2
4
```

## Dijkstra (Heap)

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

```bash
0
2
3
1
2
4
```

## Floyd Warshall

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

```bash
0 4 8 6
3 0 7 9
5 9 0 4
7 11 2 0
```

## Disjoint Sets

```python
def find_parent(parent, x):
  # 루트 노드가 아니라면, 루트 노드를 찾을 때까지 재귀적으로 호출
  if parent[x] != x:
    return find_parent(parent, parent[x])
  return x # 루트 노드

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

```bash
각 원소가 속한 집합:  1 1 1 1 5 5
부모 테이블:  1 1 2 1 5 5
```

## Disjoints Sets (Update)

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

```bash
각 원소가 속한 집합:  1 1 1 1 5 5
부모 테이블:  1 1 1 1 5 5
```

## Is Cycle

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

```bash
사이클이 발생했습니다.
```

## Kruskal

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

```bash
159
```

## Topology Sort

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

```bash
1 2 5 3 6 4 7
```
