
## 문제링크
[대장균의 크기에 따라 분류하기 1](https://school.programmers.co.kr/learn/courses/30/lessons/299307)
## 첫번째 시도
if 쓰면 일반 플밍 언어로는 쉬울텐데 sql에도 그런게 있나? 써서 스칼라 만들면 될것같다 싶었다.
찾아보니 case-when이 sql에서의 if-else에 대응한다고 한다.
```
SELECT ID, 
    CASE 
        WHEN SIZE_OF_COLONY <= 100 THEN 'LOW'
        WHEN SIZE_OF_COLONY <= 1000 THEN 'MEDIUM'
        ELSE 'HIGH'
    END AS SIZE
FROM ECOLI_DATA
ORDER BY ID;
```
## 문제점
해당 사항 없음.

## 수정된 코드
해당 사항 없음.

## 분석
### 로직
해당 사항 없음.

### 문법

#### case-when 구문
if-else의 sql버전
```
case
    when 조건 then 반환값
    else
end
```
### 참조 링크
해당사항 없음.

### AI 답변

