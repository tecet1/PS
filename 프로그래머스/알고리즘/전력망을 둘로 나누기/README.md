
## 문제링크
[전력망을 둘로 나누기](https://school.programmers.co.kr/learn/courses/30/lessons/86971)
## 첫번째 시도
```
from collections import deque

def solution(n, wires):
    '''
    잘랐을 때 두 그룹으로 나뉠 것이므로
    각 그룹에 대해 bfs돌려서 그룹 내 요소 갯수를 계산하고
    min_val = min(min_val,abs(차이))를 리턴하면 될듯
    
    bfs 연습
    인접 리스트 사용
    
    '''
    adj_list = [[] for _ in range(n+1)] # 0번째는 안씀
    answer = float('inf')
    
    for wire in wires:
        start, end = wire
        adj_list[start].append(end)
        adj_list[end].append(start)
        
    for wire in wires:
        visited = [False for _ in range(n+1)]
        current_map = adj_list.copy()
        start, end = wire
        group_size = 0
        
        current_map[start].remove(end)
        current_map[end].remove(start)
        
        #bfs
        q = deque()
        q.append(1)
        while q:
            current = q.popleft()
            if visited[current] == True:
                continue
            else: #visited[current] == False
                visited[current] = True
                group_size += 1
                for element in current_map[current]:
                    q.append(element)
        
        answer = min(answer, abs((2*group_size)-n))
        
    return answer
```
먼저 인접리스트를 만든 뒤 모든 노드를 직접 끊어보는 방식으로 완전탐색을 구현하려 했다.
노드를 끊은 뒤의 트리 구조를 current_map에 복사한 뒤, 1번 노드에서 bfs를 돌려 소속된 그룹의 총 인자 개수를 세고, min(기존의 최소값, abs(2 * 그룹 인자 개수 - n))를 돌려 최종적으로 최대한 비슷하게 나뉘어진 상태를 반영하려 했다. 

하지만 오답을 반환했고, 아마도 문제는 copy의 방식에 있을 것으로 예상한다.

## 문제점
예상대로 copy의 방식에 문제가 있었다. 리스트의 .copy() 메서드는 얕은 복사를 수행하는데, 나는 얕은 복사가 내가 구현하고자 한 '요소를 그대로 갖는 다른 객체 생성'방식인줄 알았으나, 그게 아니라 '같은 객체를 지칭하는 다른 변수명 생성'방식이었다. 즉 깊은 복사를 해야 올바르게 구현이 가능해진다.
깊은 복사를 구현하는 방법은 두가지이다.
1. copy.deepcopy() 사용
2. 그냥 원본을 사용 (노드 끊었다가 나중에 다시 붙이기)

copy는 copy 모듈을 import하는 방식인데, 이번 문제를 풀때는 불필요하여 넘어가도록 한다.
위 코드에서 current_map을 없애고 마지막에 remove했던 내용을 다시 append하여 AC를 받았다.
## 수정된 코드
```
from collections import deque

def solution(n, wires):
    '''
    잘랐을 때 두 그룹으로 나뉠 것이므로
    각 그룹에 대해 bfs돌려서 그룹 내 요소 갯수를 계산하고
    min_val = min(min_val,abs(차이))를 리턴하면 될듯
    
    bfs 연습
    인접 리스트 사용
    
    '''
    adj_list = [[] for _ in range(n+1)] # 0번째는 안씀
    answer = float('inf')
    
    for wire in wires:
        start, end = wire
        adj_list[start].append(end)
        adj_list[end].append(start)
        
    for wire in wires:
        visited = [False for _ in range(n+1)]
        start, end = wire
        group_size = 0
        
        adj_list[start].remove(end)
        adj_list[end].remove(start)
        
        #bfs
        q = deque()
        q.append(1)
        while q:
            current = q.popleft()
            if visited[current] == True:
                continue
            else: #visited[current] == False
                visited[current] = True
                group_size += 1
                for element in adj_list[current]:
                    q.append(element)
        
        answer = min(answer, abs((2*group_size)-n))
        
        adj_list[start].append(end)
        adj_list[end].append(start)
        
    return answer
```

## 분석
### 로직
인접 리스트를 사용한 bfs를 연습함.
### 문법
해당사항 없음.

> Written with [StackEdit](https://stackedit.io/).

