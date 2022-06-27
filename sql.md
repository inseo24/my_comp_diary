### UNION

레코드를 합침 - 모두 합침(중복 미포함)

UNION ALL - 모두 합침(중복 포함)

UNION MINUS - 겹치는 내용 빼고 왼쪽 것만 나옴

UNION INTERSECT - 공통분모만 나옴

### Join

컬럼을 합침

- Nested Loop Join
    - 중첩 for문과 비슷, inner table의 인덱싱 전략이 중요
- sort merge join
    - 먼저 sort를 한 후 join
- hash join
    - 배치에서 쓰면 좋음, 대용량 테이블 조인에 좋다.

- inner join
    - 관계가 있는 INNER 값들만 합침
- outer join
    - 관계가 없는 outer도 포함해 합침
- self join
    - 같은 테이블 참조
- cross join(카테시안)
    - 합집합

LEFT(왼쪽 outer 포함)/RIGHT(오른쪽 outer 포함)/FULL OUTER(양쪽 모두 포함)  

### cascade

삭제 시 참조하는 테이블도 모두 삭제

- set null : 삭제시 참조하는 컬럼만 null로 설정