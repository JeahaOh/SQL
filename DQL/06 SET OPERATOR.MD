# SET OPERATOR
조인 외에도 테이블 간의 데이터를 조회하는 방법이 있음.  
집합 연산자는 SELECT 문을 여러개 연결하여 작성,  
각 SELECT 문의 조회 결과를 하나로 합치거나 분리할 수 있음.  
즉, 합집합, 교집합, 차집합과 같음.  
  
| OPERATOR  | DESC                                 | KIND |
|:----------|:-------------------------------------|:-----|
| UNION     | 조회 결과의 합집합. 중복행은 1번만 출력.      | 합집합 |
| UNION ALL | 조회 결과의 합집합. 중복되는 행도 출력.       | 합집합 |
| INTERSET  | 조회 결과의 교집합. 중복되는 행만 출력.       | 교집합 |
| MINUS     | 첫 번째 조회 결과에서 두 번째 조회 결과를 뺀다. | 차칩합 |
```
  SELECT    열 이름
  FROM      테이블 이름
  집합 연산자   <---  UNION, UNION ALL, INTERSET, MINUS
  SELECT    열 이름
  FROM      테이블 이름
  [ORDER BY 열 이름 [ASC or DESC]]
```

- SELECT 문에서 기술한 열과 두 번째 SELECT 문에서 기술한 열은  
  왼쪽부터 순서대로 1 : 1로 대응함,  
  열 개수와 데이터 타입이 일치해야 함.  
  열의 순서가 다르거나 데이터 타입이 일치하지 않으면 에러남.  
- SELECT 문에 대한 연산은 위에서 아래로 수행됨.
- ORDER BY 절은 SELECT 문의 맨 끝에 기술함.
  
## UNION
```
SELECT COUNT(*)
FROM
  (
    SELECT  department_id
    FROM    employees
    UNION
    SELECT  department_id
    FROM    departments
    ORDER BY department_id
  );
```
  
## UNION ALL
```
SELECT COUNT(*)
FROM
  (
    SELECT  department_id
    FROM    employees
    UNION ALL
    SELECT  department_id
    FROM    departments
    ORDER BY department_id
  );
```

## INTERSECT
```
SELECT COUNT(*)
FROM
  (
    SELECT  department_id
    FROM    employees
    INTERXECT
    SELECT  department_id
    FROM    departments
    ORDER BY department_id
  );
```
## MINUS
```
SELECT COUNT(*)
FROM
  (
    SELECT  department_id
    FROM    departments
    MINUS
    SELECT  department_id
    FROM    employees
    ORDER BY department_id;
  );
```