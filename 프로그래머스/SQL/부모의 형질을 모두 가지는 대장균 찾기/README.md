
## 문제링크
[부모의 형질을 모두 가지는 대장균 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/301647)
## 첫번째 시도
```
select a.ID, a.GENOTYPE, b.GENOTYPE as PARENT_GENOTYPE
from ECOLI_DATA a join ECOLI_DATA b on a.parent_id = b.id
where (a.genotype & b.genotype) = b.genotype
order by a.id
```

비트마스킹을 통한 집합 찾기 문제이다.
이 경우, 자식이 부모의 형질을 모두 갖고 있어야 하므로 (a&b)=b를 적용했다.

## 문제점
해당 사항 없음.

## 수정된 코드
해당 사항 없음.

## 분석
### 로직
해당 사항 없음.

### 문법
#### 비트마스킹을 통한 집합관계 표현
```
a=b
동일한 집합 여부

(a&b)=b
a가 b를 포함

(a&b)>0
a가 b의 일부를 포함
```

### 참조 링크
해당사항 없음.

### AI 답변

