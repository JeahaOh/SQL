# SELECT
## SELECT 기본 문법
```
SELECT    [DISTINCT] 열 이름 [or 별칭(alias)]
FROM      테이블 이름
[WHERE    조건식]
[ORDER BY 열 이름 [ASC or DESC]];
```
  
## SQL 작성 규칙
```
SELECT
  *
FROM employees A,
  (
    SELECT *
    FROM    departments
    WHERE   department_id = 20
  )   B
WHERE A.department_id = B.department_id;
```
  
## 전체 데이터 조회하기
```
SELECT  *
FROM    employees;
```
  
## 원하는 열만 조회하고 정렬하기
```
SELECT employee_id, first_name, last_name
FROM   employees
ORDER BY  employee_id DESC;
```

## 중복된 출력값 제거하기
DISTINCT 뒤에 열이 계속 나열되면 원하는 값이 나오지 않을 수 있으니 ()를 신경 써야 함.  
```
SELECT job_id
FROM   employees;
```
```
SELECT DISTINCT( job_id )
FROM   employees;
```

## 효율적인 SQL을 위한 별칭(alias)
AS를 붙일 수도 있고, 떼도 됨.  
가독성을 위해서는 붙이는 걸 권장함.  
```
SELECT
  employee_id AS 사원번호
  ,   first_name 이름
  ,   last_name   성
FROM
  employees;
```

## 데이터 값 연결하기
연결 연산자 `||`  
[ 열 이름 ] || [ 열 이름 ] or [ 열 이름 ] '[문자]'
```
SELECT
  employee_id,
  first_name || ' ' || last_name,
  email || '@' || 'company.com'
FROM   employees;
```

## 산술 처리: 데이터 값 계산
데이터 값을 계산할 때 사용.  
산술 표현식에는 열 이름, 숫자, 날짜, 산술 연산자 등을 포함 할 수 있음.  
산술 연산자는 가감승제( +, -, *, / )가 있음.  
연산은 (), *, /, +, -순으로 함.  
  
employees 테이블에서 employee_id, salary, salary에 500을 더한 값, 100을 뺀값. 10%를 추가해서 2로 나눈값을 출력하시오.
```
SELECT
  employee_id,
  salary,
  salary + 500,
  salary - 100,
  (salary * 1.1) / 2
FROM
  employees;
```
```
SELECT
  employee_id AS 사번,
  salary AS 급여,
  salary + 500 AS 추가급여,
  salary - 100 AS 인하급여,
  (salary * 1.1) / 2 AS 조정급여
FROM
  employees;
```