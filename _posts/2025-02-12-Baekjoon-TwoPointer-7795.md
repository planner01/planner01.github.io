---
title: "Baekjoon DP 2748"
date: 2025-02-11 10:00:00 +0900
categories: [CodingTest, Algorithm]
tags: [python, Two Pointer, Algorithm]
---

### Coding Test (DP)
[백준 먹을 것인가 먹힐 것인가, 7795, 실버 3](https://www.acmicpc.net/problem/7795)

- [x] 문제 풀이 완료
- [x] 이해 완료

<img width="962" alt="Image" src="<img width="1091" alt="Image" src="https://github.com/user-attachments/assets/21d11693-7bf7-4ed0-abd9-355223221691" />" />

```python
#입력
2
5 3
8 1 7 3 1
3 6 1
3 4
2 13 7
103 11 290 215
# 출력
7
1
```


### 아이디어
> main과 sub 포인터를 사용하는 Two pointer 알고리즘 활용
> A(main),B(sub)는 오름차순 정렬
> 1. 전체 모든 수에 대해 진행할 것이므로 while main < N 반복
> 2. A[main] > B[sub] -> sub +=1 
> 3. A[main] <= B[sub] -> main +=1, count += sub
> 4. sub == M 이라면, 이미 A의 값이 B보다 무조건 큼 -> count += sub

### 기본정리
* 시간복잡도 : O(N+M)

```python
t= int(input())
for _ in range(t):
    
    N, M = map(int, input().split())
    A = list(map(int, input().split()))
    B = list(map(int, input().split()))
    result = 0
    
    A.sort()
    B.sort()

    main = 0
    sub = 0
    count = 0

    while main < N :
        if sub == M:
            count += sub
            main +=1 
        else:
            if A[main] <= B[sub]:
                main +=1
                count += sub
            elif A[main] > B[sub]:
                sub +=1
    print(count)
```

### 느낀점
* main/sub의 지정과 반복문의 종료 조건 성립이 중요

