
## 문제링크
[조건에 맞는 회원수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131535)
## 첫번째 시도
```
select count(*) as USERS
from
(SELECT user_id
from user_info
where JOINED like '2021%' and age >= 20 and age <= 29) t
```
서브쿼리를 연습할 겸 작성해봤다. 
하지만, 간단히 count()만 사용해서 구현이 가능하고, 그 편이 더 효율적이니 실전에서는 그렇게 구현하는 것이 맞는 방법이다.

## 문제점
해당 사항 없음.

## 수정된 코드
```
SELECT COUNT(*) AS USERS
FROM USER_INFO
WHERE JOINED like '2021%' #JOINED >= '2021-01-01' AND JOINED <= '2021-12-31'
  AND AGE BETWEEN 20 AND 29;
```

## 분석
### 로직
해당사항 없음.

### 문법
#### BETWEEN 
inclusive (시작값 이상과 끝값 이하)한 포함관계를 적용할 때 사용
```
변수 between 시작값 and 끝값, 
```
### 참조 링크


