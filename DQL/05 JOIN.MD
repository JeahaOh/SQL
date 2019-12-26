# JOIN
관계형 데이터베이스에서 테이블 안에 있는 행들을 논리에 땨라 연결할 수 있도록 하는 기법.  
  
|  JOIN         |  DESC                                |
|--------------:|:-------------------------------------|
| EQUI JOIN     | 조건이 정확히 일치하는 경우, 결과 출력.       |
| NON EQUI JOIN | 조건이 정확히 일치하지 않는 경우, 결과 출력.   |
| SELF JOIN     | 자체 테이블 내에서 조인.                   |
| OUTER JOIN    | 조건이 정확히 일치하지 않아도 모든 결과를 출력. |
| 곱집합 (Cartesian Product) | 가능한 모든 행을 조인.         |
  
---
## EQUI JOIN
양쪽 테이블에서 공통적으로 존재하는 컬럼 값이 일치하는 행만 가져오는 일반적인 조인.  
등호 (=) 연결 연산자를 사용해서 조건 값이 정확히 일치할 때만 행을 가져오기 때문에,  
EQUI JOIN 혹은 INNER JOIN 이라고 함.  
주로 PK와 FK의 관계를 이용해 조인하지만, 다양한 조건으로 조인할 수 있음.  
  
```
  SELECT  A.열 이름1, B.열 이름 2
  FROM    테이블 1 A, 테이블 2 B
  WHERE   테이블 1.열 이름 = 테이블 2.열 이름
```
```
SELECT *
FROM
  employees A, departments B
WHERE
  A.department_id = B.department_id;
```
```
SELECT A.employee_id, A.department_id, B.department_name, C.location_id, C.city
FROM
  employees A, departments B, locations C
WHERE
  A.department_id = B.department_id
AND
  B.location_id = C.location_id
```

## NON-EQUI JOIN
대상 테이블 간 동일 칼럼 없이, 다른 조건으로 조인할 때 사용.  
같은 조건이 아닌 크거나 작은 경우 JOIN을 수행하는 방법.  
```
SELECT
  A.employee_id, A.first_name, A.salary,
  B.grade
FROM
  employees A, salarygrade B
WHERE
  A.salary BETWEEN B.losalary AND B.hisalary;
```
HR 테이블에서는 적절한 예제가 없다.  
위 예제도 salarygrade라는 테이블이 따로 필요함.  
정상은 아님.  
  
---

## SELF JOIN
자기 자신의 테이블을 조인하는 것.
```
  SELECT  A.열 이름, B.열 이름
  FROM    테이블 1 A, 테이블 1 B
  WHERE   테이블 1.열 이름 1 = 테이블 1.열 이름 2
```
```
SELECT
  A.employee_id, A.first_name, A.last_name, A.manager_id,
  B.first_name|| ' ' ||B.last_name AS manager_name
FROM
  employees A, employees B
WHERE
  A.manager_id = B.employee_id
ORDER BY
  A.employee_id;
```
  
---

## OUTER JOIN
조건을 만족하지 않는 행도 모두 출력하기 위해 사용.  
조인시 값이 없는 테이블 측에 (+)연산자를 붙임.
```
  SELECT  A.열 이름1, B.열 이름 2
  FROM    테이블 1 A, 테이블 2 B
  WHERE   테이블 1.열 이름 = 테이블 2.열 이름(+)
```
```
SELECT
  A.employee_id, A.first_name, A.last_name,
  B.department_id, B.department_name
FROM
  employees A, departments B
WHERE
  A.department_id = B.department_id(+)
ORDER BY
  A.employee_id DESC
```
```
SELECT
  A.employee_id, A.first_name, A.last_name,
  B.department_id, B.department_name
FROM
  employees A, departments B
WHERE
  A.department_id(+) = B.department_id
ORDER BY
  A.employee_id DESC
```

---

## ANSI JOIN
ANSI / ISO SQL 표준인 LEFT OUTER JOIN, RIGHT OUTER JOIN, FULL OUTER JOIN을 지원.  
ANSI JOIN이 명시적을 표형하기 때문에 더 가독성이 좋은 느낌.  

### INNER JOIN
그냥 묶을 때 사용.  
INNER 생략 가능.
```
SELECT  DISTINCT(E.department_id), D.department_id
FROM    employees E
INNER JOIN departments D
ON      E.department_id = D.department_id;
```
  
### LEFT OUTER JOIN
(+) 기호 대신 명시적으로 사용.  
오른쪽 테이블에 조인 시킬 값이 없는 경우 사용.  
```
SELECT  DISTINCT(E.department_id), D.department_id
FROM    employees E
LEFT OUTER JOIN departments D
ON      E.department_id = D.department_id;
```
  
### RIGHT OUTER JOIN
왼쪽 테이블에 조인 시킬 값이 없는 경우 사용.
```
SELECT  DISTINCT(E.department_id), D.department_id
FROM    employees E
RIGHT OUTER JOIN departments D
ON      E.department_id = D.department_id;
```
  
### FULL OUTER JOIN
양쪽 모두 OUTER JOIN을 걸어야 하는 경우 사용.
```
SELECT  DISTINCT(E.department_id), D.department_id
FROM    employees E
FULL OUTER JOIN departments D
ON      E.department_id = D.department_id;ㅋ
```

---
cross join은 뭐지?
---