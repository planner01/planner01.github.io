---
title: "Backjoon BFS/DFS 2667"
date: 2025-02-11 10:00:00 +0900
categories: [Coding Test]
tags: [python, DFS, BFS]
---

### Coding Test (DFS/BFS)
[백준 단지번호 붙이기, 2667, 실버 1](https://www.acmicpc.net/problem/2667)

- [x] 문제 풀이 완료
- [x] 이해 완료

<img width="1061" alt="Image" src="https://github.com/user-attachments/assets/dee49d0c-e580-48c7-a59a-aeecb8e75d97" />

```python
#입력
7
0110100
0110101
1110101
0000111
0100000
0111110
0111000
```
```python
# 출력
3
7
8
9
```

### 아이디어
>DFS/BFS의 기본은 특정 Map or Graph에서 한 좌표를 기반으로 전체 영역 혹은 일부 영역을 재귀함수를 통해 순환하며 정답을 찾아가는 방식.

* 방문하지 않았으며, 좌표값이 0이 아닌 점을 기준으로 DFS/BFS를 수행한다.
* DFS/BFS 수행 시 방문한 좌표의 개수(아파트 단지 수)를 Count한 후 함수가 종료될 때 마다 Count 값 Return
* DFS/BFS를 둘 다 활용하여 문제를 풀어본다.

### 기본정리
* 시간복잡도 : O(V+E)
* V(Vertex), E(Edge) = N^2, 4N^2
* V+E = 5N^2 ~= N^2 ~= 625 < 2억(시간제한 1초) >> 가능

### DFS
```python
import sys

input = sys.stdin.readline

N = int(input())
graph = []
visited = [[False]*(N) for _ in range(N)]

each_cnt = 0
apart_group = []
for i in range(N):
    graph.append(list(map(int, input().strip())))

dx = [1,0,-1,0]
dy = [0,1,0,-1]

def dfs(x,y):
    global each_cnt
    each_cnt += 1 
    # 동작 2. 현재 노드를 방문처리
    visited[x][y] = True

    # 동작 3. 현재 노드에서 상하좌우를 둘러보며, 방문하지 않았으며 현재 노드와 값이 동일한 노드 탐색
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        # 동작 4. 조건 만족하는 노드 발견시 해당 노드를 기점으로 다시 DFS 수행
        if 0<= nx < N and 0<= ny < N:
            if visited[nx][ny] == False and graph[nx][ny] == graph[x][y]:
                visited[nx][ny] = True
                dfs(nx, ny)
    return each_cnt

for i in range(N):
    for j in range(N):
      # 동작 1.전체 map을 돌면서,방문하지 않았으며 0이 아닌 노드를 탐색, 노드 발견시 해당 노드를 기점으로 DFS 수행
        if visited[i][j] == False and graph[i][j] != 0:
            apart_group.append(dfs(i,j))
            each_cnt = 0

print(len(apart_group))
apart_group.sort()
for i in apart_group:
    print(i)
```

### BFS
```python
import sys
from collections import deque

input = sys.stdin.readline
N = int(input())
graph = []
visited = [[False] * N for _ in range(N)]

for _ in range(N):
    graph.append(list(map(int, input().strip())))

dx = [1,0,-1,0]
dy = [0,1,0,-1]

# 동작 1. 현재 노드 방문처리 및 queue에 입력함으로써 재귀함수 구현
def bfs(x,y):
    visited[x][y] = True

    global each_cnt

    q = deque()
    q.append((x,y))
    while q:
        ex, ey = q.popleft()
        for i in range(4):
            nx = ex + dx[i]
            ny = ey + dy[i]
            # 동작 2. 조건에 성립하는 노드 발견시 queue에 append함으로써 재귀함수가 돌아갈 수 있도록 구현
            if 0<= nx < N and 0<= ny < N:
                if visited[nx][ny] == False and graph[ex][ey] == graph[nx][ny]:
                    visited[nx][ny] = True
                    q.append((nx,ny))
                    each_cnt +=1 
    return each_cnt

each_cnt = 1
apart_group = []

for i in range(N):
    for j in range(N):
        if visited[i][j] == False and graph[i][j] !=0:
            visited[i][j] = True
            apart_group.append(bfs(i,j))
            each_cnt = 1

print(len(apart_group))
apart_group.sort()
for i in apart_group:
    print(i)
```

### 느낀점
* DFS/BFS에 입문하기에 좋은 예제. 
* 문제 해결은 완료, 하지만 각 변수 및 함수 동작이 어떻게 이루어지는지에 대해 완벽한 이해 필요.

