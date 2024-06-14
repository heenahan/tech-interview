## 1. Key (기본키, 후보키, 슈퍼키 등등...) 에 대해 설명해 주세요.
- 슈퍼키(super key)
relation에서 tuples를 unique하게 식별할 수 있는 attributes set
- 후보키(candidate key)
어느 한 attribute라도 제거하면 unique하게 tuples를 식별할 수 없는 super key
- 기본키(primary key)
relation에서 tuples를 unique하게 식별하기 위해 선택된 candidate key
- unique key
primary key가 아닌 candidate keys
- foreign key
다른 relation PK를 참조하는 attributes set
- 제약 조건(constraints)
relational database의 relations들이 언제나 항상 지켜줘야 하는 제약 사항
    - domain constraints
        attribute의 value는 해당 attribute의 domain에 속한 value여야 한다.
    - key constraints
        서로 다른 tuples는 같은 value의 key를 가질 수 없다.
    - null value constraints
        attribute가 not null로 명시되었다면 null값으로 가질 수 없다
    - entity integrity constraint
        primary key는 value에 null을 가질 수 없다.
    - referential integrity constraint
        FK와 PK와 도메인이 같아야 하고 PK에 없는 values를 FK가 값으로 가질 수 없다.
## IN, EXISTS, ANY, ALL 연산자
- IN
    - v IN(v1, v2, v3 ...)란 v가 (v1, v2, v3 ...) 중에 하나와 값이 같다면 TRUE를 return한다.
    - (v1, v2, v3 ...)는 명시적인 값들의 집합일수도 있고 subquery의 결과(set or multiset)일 수도 있다.
- NOT IN
    - v NOT IN(v1, v2, v3 ...)는 v가 (v1, v2, v3 ...)의 모든 값과 값이 다르다면 TRUE를 return한다.
- EXISTS
    - exists는 subquery의 결과가 최소 하나의 row라도 있다면 TRUE를 반환한다.
- NOT EXISTS
    - not exists는 subquery의 결과가 단 하나의 row도 없다면 TRUE를 반환한다.
- ANY
    - v comparison_operator ANY (subquery)는 subquery가 반환한 결과들 중에 단 하나라도 v와의 비교 연산이 TRUE라면 TRUE를 반환한다.
    - SOME도 ANY와 같은 역할을 한다.
- ALL
    - v comparison_operator ALL (subquery)는 subquery가 반환한 결과들과 v의 비교 연산이 모두 TRUE라면 TRUE를 반환한다.
## 3. NULL
- unkwon
- unavailable or withheld
- not applicable 

NULL에 대해서 IS, IS NOT라는 연산자를 사용해야한다.
SQL에서 NULL과 비교 연산을 하게 되면 그 결과는 UNKNOWN이다. UNKNOWN은 TRUE일수도 있고 FALSE일수도 있다라는 의미이다. 결국 비교/논리 연산의 결과로 TRUE, FALSE, UNKNOWN을 가진다.

where절에 있는 condition의 결과가 TRUE인 tuple만 선택된다. 즉, 결과가 FALSE이거나 UNKNOWN이면 tuple은 선택되지 않는다.

그래서 NOT IN 사용 시 주의해야할 점이 있다. v not in (v1, v2, v3)는 풀어쓰면, v != v1 and v != v2 and v != v3이다. 그런데 3 not in (1, 2, NULL)일 경우 UNKOWN이 된다.