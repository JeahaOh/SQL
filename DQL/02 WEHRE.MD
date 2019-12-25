# 조건 절 WHERE를 활용한 데이터 검색
- 원하는 결과를 얻기위해 조건을 제한함.
- WHERE절은 FROM절 다음에 위치한다.  
- 문자열, 날짜는 'Single Quotation'안에 표기해야 함.
  - 명령어는 대소문자 구분을 하지 않지만,  
    테이블 내에 저장된 데이터 값은 대소문자를 구분함.
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
|:----:|:-----------:|:-------------:|
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
## BETWEEN
```
SELECT
  *
FROM employees
WHERE
  salary BETWEEN 10000 AND 20000;
```
  
## IN
```
SELECT
  *
FROM employees
WHERE
  salary IN (10000, 17000, 24000);
```
  
## LIKE와 '%'
```
SELECT
  *
FROM employees
WHERE
  job_id LIKE 'AD%';
```

## '_'
```
SELECT
  *
FROM employees
WHERE
  job_id LIKE 'AD___';
```

## IS NULL
```
SELECT
  *
FROM employees
WHERE
  manager_id IS NULL;
```
    
    
# 논리 연산자 : 조건 논리를 계속 연결하기
## AND
```
SELECT
  *
FROM employees
WHERE
  salary > 4000
AND
  job_id = 'IT_PROG'
```
  
## OR
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
  
## !=와 <>
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

## IS NOT NULL
```
SELECT
  *
FROM employees
WHERE
  manager_id IS NOT NULL
```
