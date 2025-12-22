
## 문제링크
[대장균들의 자식의 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/299305)
## 첫번째 시도
```
select ID, ifnull(c.cnt,0) as CHILD_COUNT
from ecoli_data
left join (
    select parent_id as p_id, count(*) as cnt
    from ECOLI_DATA
    group by parent_id
) as c 
on id = c.p_id
order by id
```

## 문제점
해당 사항 없음.

## 수정된 코드
해당 사항 없음.

## 분석
### 로직
해당 사항 없음.

### 문법
카테시안 곱은 cross join으로 만들 수 있고, 이렇게 하면 팀원들에게 카테시안 곱을 의도적으로 사용했음을 알려줄 수 있다.
#### ifnull()
```
ifnull(c.cnt,0)
```
#### left join
left join은 왼쪽 개체는 모두 가지도록 join하는 문법이다.

### 참조 링크
해당사항 없음.

### AI 답변


