
## 문제링크
[특정 물고기를 잡은 총 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/298518)
## 첫번째 시도
1. 카테시안 곱
```
select count(*) as FISH_COUNT
from FISH_INFO i ,FISH_NAME_INFO n 
where i.FISH_TYPE = n.FISH_TYPE and n.fish_name in ('bass', 'snapper')
```

2. join
```
select count(*) as FISH_COUNT
from FISH_INFO i join FISH_NAME_INFO n on i.FISH_TYPE = n.FISH_TYPE
where n.fish_name in ('bass', 'snapper')
```

3. exists
```
select count(*) as FISH_COUNT
from FISH_INFO as i
where exists (
    select 1
    from fish_name_info as n
    where i.FISH_TYPE = n.FISH_TYPE
    and n.FISH_NAME in ('BASS', 'SNAPPER')
)
```

## 문제점
해당 사항 없음.

## 수정된 코드
해당 사항 없음.

## 분석
### 로직
#### 비트 연산 기반의 집합 관리
```
where (d.SKILL_CODE & s.CODE) > 0
and s.name in ('python', 'c#')
```
먼저 카테시안 곱을 만들고 각 row에 대해 and연산을 수행해서 1인 경우를 찾는 코드로, 집합에 포함되는지 여부를 알 수 있다.

### 문법
카테시안 곱은 cross join으로 만들 수 있고, 이렇게 하면 팀원들에게 카테시안 곱을 의도적으로 사용했음을 알려줄 수 있다.
```
SELECT s.size_name, c.color_name
FROM sizes s
CROSS JOIN colors c; -- 모든 조합 생성
```

### 참조 링크
해당사항 없음.

### AI 답변


