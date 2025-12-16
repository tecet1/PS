
## 문제링크
[피로도](https://school.programmers.co.kr/learn/courses/30/lessons/87946)
## 첫번째 시도
```
from itertools import permutations

def solution(k, dungeons):
    '''
    예제에서 소모 피로도 기준으로 2->0->1 순으로 순회가 가능하여 그리디 문제인줄 알았으나, 
    만약 0번 리스트가 [100,20]이 되면 그렇게 풀 수 없게 되므로 다른 방법을 생각해 보기로 했다.
    
    dfs문제인가?
    [1,2,3 1,3,2 2,1,3 2,3,1 3,1,2 3,2,1] 총 여섯가지 -> 또 순열문제인가?
    순열로 순회하는 경우의 수를 열거한 뒤 각 순열에 대해 다시 순회하면 될 것 같음
    '''
    
    perm = permutations(dungeons)
    max_traversed_dungeons = 0
    
    for p in perm:
        stamina = k
        flag = 1
        current_traversed_dungeons = 0
        for dungeon in p:
            if stamina >= dungeon[0] and flag == 1:
                current_traversed_dungeons += 1
            if stamina < dungeon[0]:
                flag = 0
            stamina -= dungeon[1]
        max_traversed_dungeons = max(max_traversed_dungeons,current_traversed_dungeons)
            
    return max_traversed_dungeons
```
순열을 구현하는 또다른 문제여서
전에 배웠던 itertool.permutations를 써서 구현했다.

## 수정된 코드
해당사항 없음.

## 분석
### 로직
해당사항 없음.

### 문법
해당사항 없음.

> Written with [StackEdit](https://stackedit.io/).

