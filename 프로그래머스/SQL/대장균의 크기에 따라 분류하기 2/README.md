
## 문제링크
[대장균의 크기에 따라 분류하기 2](https://school.programmers.co.kr/learn/courses/30/lessons/301649)
## 첫번째 시도
1. percent_rank() 윈도우 함수
```
SELECT ID, 
    CASE 
        WHEN perc <= 0.25 THEN 'CRITICAL'
        WHEN perc <= 0.5 THEN 'HIGH'
        WHEN perc <= 0.75 THEN 'MEDIUM'
        ELSE 'LOW'
    END AS COLONY_NAME
FROM (
    select id, percent_rank() over (ORDER BY SIZE_OF_COLONY desc) as perc
    from ECOLI_DATA
) sub
ORDER BY ID;
```

2.ntile() 윈도우 함수
```
SELECT ID, 
    CASE 
        WHEN q = 1 THEN 'CRITICAL'
        WHEN q = 2 THEN 'HIGH'
        WHEN q = 3 THEN 'MEDIUM'
        ELSE 'LOW'
    END AS COLONY_NAME
FROM (
    select id, ntile(4) over (ORDER BY SIZE_OF_COLONY desc) as q
    from ECOLI_DATA
) sub
ORDER BY ID;
```

둘다 동일한 결과를 반환하는데, percent_rank() 쪽이 좀 더 유연한 것 같다.

## 문제점
해당 사항 없음.

## 수정된 코드
해당 사항 없음.

## 분석
### 로직
해당 사항 없음.

### 문법
#### 상위 n%의 표현
```
percent_rank() over (order by attribute desc) as perc
상위 %를 반환

ntile(n) over (order by attribute desc) as q
n분위수를 반환
```

### 참조 링크
해당사항 없음.

### AI 답변

