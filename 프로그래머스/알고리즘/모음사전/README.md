
## 문제링크
[모음사전](https://school.programmers.co.kr/learn/courses/30/lessons/84512)
## 첫번째 시도
```
from functools import cmp_to_key
from itertools import product

def lexicographical_order(a,b):
    if a+b > b+a:
        return 1
    elif a+b < b+a:
        return -1
    else:
        return 0

def solution(word):
    dictionary = set()
    for i in range(1,6):
        prod = product("AEIOU",repeat = i)
        for p in prod:
            dictionary.add("".join(p))
            
    dictionary = list(dictionary)
    dictionary.sort(key=cmp_to_key(lexicographical_order))
    print(len(dictionary))
    for i in range(len(dictionary)):
        if word == dictionary[i]:
            return i

```
먼저 AEIOU문자열로 만들 수 있는 중복순열들을 집합에 넣고 집합을 리스트로 형변환 한뒤 사전순으로 정렬하여 해결하려 하였으나, 생각해보면, A와 AA의 비교를 수행한다면 이 두개는 같은 순번으로 인식되며 들어온 순서대로 정렬이 될 것임을 예상할 수 있다. 그래서 AI한테 도움을 요청했다.

## 문제점
어이없게도, 문제는 정렬을 위해 새롭게 정의한 정렬함수가 맞았는데, 수정사항으로 제시된 것이 그냥 key를 지정할 필요없이 sort()를 쓰면 된다는 것이었다. sort()가 기본적으로 일반적인 사전순 정렬을 지원하기 때문이다. 따라서 cmp_to_key를 import하고 새로 정렬함수를 정의할 필요가 없다.
## 수정된 코드
```
from itertools import product

def solution(word):
    dictionary = set()
    for i in range(1,6):
        prod = product("AEIOU",repeat = i)
        for p in prod:
            dictionary.add("".join(p))
            
    dictionary = list(dictionary)
    dictionary.sort()
    print(len(dictionary))
    for i in range(len(dictionary)):
        if word == dictionary[i]:
            return i+1
```

## 분석
### 로직
itertools에는 순열,조합,중복순열,중복조합을 각각 permutations, combinations, product, combinations_with_replacement로 지원한다. 필요할 때 import해서 사용하면 될듯.
```
itertools.permutations(iterable, r=None)
itertools.combinations(iterable, r)
itertools.product(iterable, repeat=r)
itertools.combinations_with_replacement(iterable, r)
```
그리고 이 모든 행위를 dfs를 통해 구현할 수 있다. 

### 문법
해당사항 없음.

> Written with [StackEdit](https://stackedit.io/).

