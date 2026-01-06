---
title: "Solving coding problems Array and List"
date: 2026-01-06
toc: true
toc_sticky: true
use_math: true
categories:
  - algorithms
---
# 배열, 리스트 이론
배열
- 인덱스를 이용하여 값에 접근 가능
- 삭제, 삽입 어려움 (해당 인덱스 값 옮겨야)
- 배열의 크기는 선언할때 지정하고 못바꿈
- 구조 간단

리스트
- 인덱스가 없으므로 head 포인터부터 순서대로 접근
- 포인터로 연결되어 있어서 삽입, 삭제 연산 빠름
- 선언할때 크기 지정안해도됨, 크기가 정해져있는게 아님
- 포인터를 저장할 공간도 필요해서 배열보단 복잡

# 문제
## BOJ

<details>
  <summary>11720번</summary>
  
  <div markdown="1">

  [11720번 문제 링크](https://www.acmicpc.net/problem/11720)
  ```python
  # Method 1
  n= int(input())
  nums = input() # string으로 들어감
  sum = 0
  
  for i in nums:
    sum += int(i)
  print(sum)
  ```

  ```python
  # Method 2
  n = input() 
  print(sum(map(int, input())))

  ```

  </div>
</details>

<details>
 <summary>1546번</summary>
 <div markdown="1">
 
 [1546번 문제 링크](https://www.acmicpc.net/problem/1546)

 ```python
 n = int(input()) # 과목갯수 n에 
 mylist = list(map(int, input().split()))# my_list 에 성적
 myMax = max(mylist)# myMax 에 최댓값
 sum = sum(mylist)# sum에 총합
 print(sum * 100 / myMax / n)# 새 평균(수학으로 간소화)
 ```
 </div>
</details>


