---
title: "Stack and Queue"
date: 2026-01-10
toc: true
toc_sticky: true
use_math: true
categories:
  - algorithms
---


# Stack
- Stack은 LIFO구조이다. LIFO는 삽입과 삭제가 한쪽에서만 일어난다.
- 파이썬에선 리스트를 이용하여 쉽게 스택을 구현할 수 있다. 

# Queue
- FIFO구조이다. 삽입과 삭제가 양방향에서 일어난다.
- 삭제는 front에서, 새 값 추가는 rear에서 일어난다. 
- 파이썬에선 deque를 이용하여 구현한다. 


## [BOJ] 10828

- `push` : 정수 $x$ 를 스택에 넣는 연산.
- `pop` : 가장 위에 있는 정수를 출력하면서 뺌. (없으면 $-1$)
- `size` : 스택에 들어있는 정수의 개수 확인
- `empty` : 비어있으면 1, 값이 있으면 0
- `top` : 가장 위에 있는 값 확인 (비어있으면 $-1$)

위의 연산들은 모두 $O(1)$ 안에 구현되어야 한다. 

```python 
import sys
input = sys.stdin.readline

n = int(sys.stdin.readline())

stack = [] 

for _ in range(n):
    command = sys.stdin.readline().split()
    cmd_type = command[0]
    
    if cmd_type == 'push':
        stack.append(int(command[1]))
    elif cmd_type =='pop':
        print(stack.pop()) if stack else print(-1)
    elif cmd_type == 'size':
        print(len(stack))
    elif cmd_type == 'empty':
        print(1) if not stack else print(0)
    elif cmd_type == 'top':
        print(-1) if not stack else print(stack[-1])
```

## [BOJ] 1874

## [BOJ] 17298

## [BOJ] 2164

## [BOJ] 11286