# SUBQUERY
두 번 작성해서 결과를 출력해야 하는 SELECT 문을 한 번만 작성해서 처리할 수 있도록 함.  
SELECT 안에 포함된 하나의 SELECT 가 있는 쿼리문.  
쿼리문 전체를 메인 쿼리라 하고, 안에 있는 쿼리를 SUBQUERY라고 함.  
복잡한 쿼리를 작성할 때 필수로 사용됨.  
메인 쿼리가 실행되기 이전에 한번만 실행됨.  
단일행 쿼리와 다중행 쿼리로 나뉨.  

- SUBQUERY는 괄호`()`로 묶어서 사용함. 메인 쿼리는 묶을 필요 없음.
- 메인 쿼리와 서브쿼리를 연결하기 위해 단일 행 연산자나 다중 행 연산자를 사용함.
- 메인 쿼리와 서브쿼리의 연결 형태는 연산자에 따라 의미가 다름.
- 메인 쿼리는 연산자의 왼쪽에 기술하고, 서브쿼리는 연산자의 오른쪽에 기술함.
- 서브쿼리에서 메인 쿼리의 순서로 SELECT 문이 실행됨.
- 서브쿼리의 서브쿼리로 중첩해서 작성할 수 있음.
  
## SUBQUERY의 종류
  
|  종류  | DESC                       |
|-------|----------------------------|
| 단일 행 | 하나의 행을 검색하는 서브쿼리     |
| 다중 행 | 하나 이상의 행을 검색하는 서브쿼리 |
| 다중 열 | 하나 이상의 열을 검색하는 서브쿼리 | 
  
## SUBQUERY의 종류에 따라 사용하는 연산자
  
| 연산자 구분 | 종류                          | 사용처          |
|----------|------------------------------|---------------|
| 단일 행    | =, >, >=, <, <=, <>, !=      | 단일 행, 다중 열 |
| 다중 행    | IN, NOT IN, EXISTS, ANY, ALL | 다중 행, 다중 열 |

## 단일 행 서브쿼리
수행 결과가 오직 하나의 로우(행)만을 반환하는 것.  
서브쿼리를 수행한 결과가 1건만 나오고,  
이 결과를 메인 쿼리로 전달해서 메인 쿼리를 수행하게 됨.  
```
SELECT  *
FROM    employees A
WHERE
  A.salary
  = (
    SELECT  salary
    FROM    employees
    WHERE   last_name = 'De Haan'
  );
```
만약 서브쿼리의 결과가 하나 이상인 경우 다중 행 서브쿼리를 사용해야 함.

## 다중 행 서브쿼리
하나 이상의 결과 행을 메인 쿼리에 전달하는 경우에 사용.  
  
| 연산자   | DESC                | EX                                    |
|--------|---------------------|---------------------------------------|
| IN     |  같은 값             | IN(10, 20)     ; 10이나 20이 포함         |
| NOT IN |  같은 값이 아닌        | NOT IN(10, 20) ; 10이나 20에 포함되지 않음  |
| EXISTS |  값이 있으면 반환       | EXISTS(10)     ; 10이 존재하면 참         |
| ANY    |  하나라도 만족하는 (OR) |  ANY(10, 20)   ; 10이나 20이 포함         |
| ALL    |  모두 만족하는 것 (AND) | ALL(10, 20)    ; 10과 20이 포함          |

```
SELECT  *
FROM    employees A
WHERE
  A.salary
  IN (
    SELECT  MIN(salary)
    FROM    employees
    GROUP BY department_id
  )
ORDER BY A.salary DESC;
```

## 다중 열 서브쿼리
메인 쿼리와 서브쿼리를 비교하는 WHERE 조건식에서 비교되는 열이 여러 개일 때 사용.
```
  SELECT    열 이름
  FROM      테이블 이름
  WHERE (열 이름1, 2, ...) IN (
                              SELECT  열 이름1, 열 이름2
                              FROM    테이블 이름
                              WHERE   조건식
                            )
```
- job_id별로 가장 낮은 salary 가 얼마인지 찾아보고, 찾아낸 job_id별 salary에 해당하는 직원이 누구인가
```
SELECT  A.employee_id, A.job_id, A.salary
FROM    employees A
WHERE
  (A.job_id, A.salary) 
  IN (
    SELECT  job_id, MIN(salary)
    FROM    employees
    GROUP BY job_id
  )
ORDER BY A.salary DESC;
```

## FROM절 SUBQUERY
FROM 절에서 SUBQUERY를 사용할 수 있음.  
```
  SELECT  column
  FROM    table1 AS 1,
          ( SELECT column
            FROM   table
            WHERE  조건식
          ) AS 2
  WHERE
    1.column = 2.column
```
```
SELECT  *
FROM    employees A, (
            SELECT  department_id AS department_id
            FROM    departments
            WHERE   department_name = 'IT' ) B
WHERE   A.department_id = B.department_id;
```