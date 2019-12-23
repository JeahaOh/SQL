# 조건 절 WHERE를 활용한 데이터 검색
- 조회하려는 조건은 지정할 수 있다.  
- WHERE절은 FROM절 다음에 위치한다.  
- 수행될 조건 절에는 비교 연산자, SQL 연산자, 논리 연산자, 열 이름, 표현식, 숫자, 문자 등 사용 가능.
```
  SELECT  열 이름    <-- 출력 하려는 열
  FROM    테이블 이름 <-- 참조 하려는 테이블
  WHERE   원하는 조건 <-- 조건 식
```
- 데이터가 조회되는 논리 순서
  1. FROM  : 참조하려는 테이블로부터
  2. WHERE : 해당하는 조건이 맞는
  3. SELECT: 열을 선택해서 조회

## WHERE절에 사용하는 연산자의 종류  
  
| 연산자 |     설명     | 예시           |
|------|-------------|---------------|
| 비교  |  조건을  비교  | =, <, > 등     |
| SQL  | 비교 조건 확장 | BETWEEN, IN 등 |
| 논리  | 논리 조건 연결 | AND, OR        |

## 연산자의 우선 순위
괄호 > 부정 연산 > 비교 연산 > SQL 연산  
NOT > AND > OR 순  
연산자의 순서는 데이터 조회 속도에 영향을 미침 -> 고급 SQL 영역임.

# 비교 연산자 : 비교 조회 조건 주기
```
SELECT *
FROM  employees
WHERE employee_id = 100;
```
```
SELECT *
FROM  employees
WHERE first_name = 'David';
```
```
SELECT
  *
FROM employees
WHERE employee_id >= 105;
```

# SQL 연산자 : 조회 조건 확장하기
```
SELECT
  *
FROM employees
WHERE
  salary BETWEEN 10000 AND 20000;
```
```
SELECT
  *
FROM employees
WHERE
  salary IN (10000, 17000, 24000);
```
```
SELECT
  *
FROM employees
WHERE
  job_id LIKE 'AD%';
```
```
SELECT
  *
FROM employees
WHERE
  job_id LIKE 'AD___';
```
```
SELECT
  *
FROM employees
WHERE
  manager_id IS NULL;
```
# 논리 연산자 : 조건 논리를 계속 연결하기
```
SELECT
  *
FROM employees
WHERE
  salary > 4000
AND
  job_id = 'IT_PROG'
```
```
SELECT
  *
FROM employees
WHERE
  salary > 4000
AND
  job_id = 'IT_PROG'
OR
  job_id = 'FL_ACCOUNT'
```
```
SELECT
  *
FROM employees
WHERE
  employee_id != 105
```
```
SELECT
  *
FROM employees
WHERE
  employee_id <> 105
```
```
SELECT
  *
FROM employees
WHERE
  manager_id IS NOT NULL
```
