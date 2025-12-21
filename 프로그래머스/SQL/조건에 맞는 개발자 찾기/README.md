
## 문제링크
[조건에 맞는 개발자 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/276034)
## 첫번째 시도

```
select distinct ID,EMAIL,FIRST_NAME,LAST_NAME
from DEVELOPERS as d, skillcodes as s
where (d.SKILL_CODE & s.CODE) > 0
and s.name in ('python', 'c#')
order by id asc
```
이 문제는 개발자가 가진 스킬을 비트마스킹해서 보유한 스킬 중 파이썬이나 C#이 있는 개발자를 찾는 문제이다.

참고로 아래와 같이 join을 사용해 풀 수도 있다고 한다.
```
SELECT DISTINCT d.ID, d.EMAIL, d.FIRST_NAME, d.LAST_NAME
FROM DEVELOPERS d
JOIN (
    SELECT CODE 
    FROM SKILLCODES 
    WHERE NAME IN ('Python', 'C#')
) s ON (d.SKILL_CODE & s.CODE) > 0
ORDER BY ID ASC;
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
해당사항 없음.

### 참조 링크
해당사항 없음.

### AI 답변

