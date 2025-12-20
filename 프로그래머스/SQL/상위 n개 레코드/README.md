
## 문제링크
[상위 n개 레코드](https://school.programmers.co.kr/learn/courses/30/lessons/59405)
## 첫번째 시도
```
SELECT NAME
from ANIMAL_INS
order by datetime asc
limit 1
```
limit을 사용해서 정렬된 데이터 중 가장 상위 n개의 값들을 가져올 수 있다.
서브쿼리나 윈도우 함수를 통해서도 구현이 가능하다.

## 문제점
해당 사항 없음.

## 수정된 코드
서브쿼리 사용(where 절)
```
SELECT NAME
FROM ANIMAL_INS
WHERE DATETIME = (SELECT MIN(DATETIME) FROM ANIMAL_INS)
```

윈도우 함수 사용 (mySQL 8.0이상에서 지원)
```
SELECT NAME
FROM (select *, rank() over (order by datetime) as rnk from animal_ins) as t
WHERE rnk = 1
```

## 분석
### 로직
SQL에서 서브쿼리를 사용하는 방법은 크게 세가지이다.
1. select 절에서 사용하는 스칼라 서브쿼리
```
SELECT 
    NAME, 
    SALARY,
    (SELECT AVG(SALARY) FROM EMPLOYEES) AS COMPANY_AVG
FROM EMPLOYEES;
```

2. from 절에서 사용하는 인라인 뷰
```
SELECT t.DEPT_NAME, t.TOTAL_SALARY
FROM (
    SELECT DEPT_NAME, SUM(SALARY) AS TOTAL_SALARY 
    FROM EMPLOYEES 
    GROUP BY DEPT_NAME
) AS t
WHERE t.TOTAL_SALARY > 10000000;
```

3. where 절에서 사용하는 서브쿼리
```
-- 평균 급여보다 많이 받는 사람들만 조회
SELECT * FROM EMPLOYEES
WHERE SALARY > (SELECT AVG(SALARY) FROM EMPLOYEES);

-- '서울'에 거주하는 고객들의 주문 내역만 조회
SELECT * FROM ORDERS
WHERE CUSTOMER_ID IN (SELECT ID FROM CUSTOMERS WHERE CITY = '서울');
```

그런데 서브쿼리는 일반적으로 join을 사용할 때에 비해 성능면에서 열등하다고 한다.
그 이유는 서브쿼리 역시 쿼리이기에 join으로 한번에 데이터를 합친뒤 찾는 것보다 연산량이 많을 수 밖에 없기 때문이다. 

복잡한 집계 연산을 실행해야하는 경우 인라인 뷰나 where문에서 조건 충족 판단을 위한 서브쿼리를 통해 미리 결과 값을 추려낸 뒤 join을 하는 경우도 있다고 한다.

### 문법
### limit n 
파이썬 판다스의 dataframe 메서드인 head와 비슷하게, 상위 n개의 값을 가져온다.

### 참조 링크
[[mysql] subquery (서브쿼리) 종류 - 스칼라 서브쿼리, 인라인 뷰, 서브쿼리](https://blog.naver.com/writer0713/222277186069)
[[SQL] 윈도우 함수(Window Function)의 소중함을 느껴보자](https://schatz37.tistory.com/12)

