# 데이터 조회 SELECT
- SQL 명령어는 여러개의 절이 모여 하나의 문장을 구성.  
  `;`으로 마쳐야 함.
- 대소문자 구분은 하지 않으나,  
  명령어나 함수등 키워드는 대문자,  
  나머지는 소문자로 구성하면 가독성이 높아짐.
- 기본벅으로 SELECT와 FROM으로 구성.
  - SELECT : 출력 하고자 하는 column의 이름을 기술.
  - FROM   : 조회하고자 하는 테이블의 이름을 기술
  
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
  
## 원하는 열만 조회하기
```
SELECT employee_id, first_name, last_name
FROM   employees
ORDER BY  employee_id DESC;
```

# ORDER BY 절로 정렬하기
정렬 하기 위해 ORDER BY 절을 사용함.  
어떤 열을 기준으로 정렬할 것인지 명시함.  
날짜, 문자, 숫자 모두 가능함. 두번 이상 제시할 경우 앞부분의 조건에서 동일 충족시 뒷부분 조건으로 정렬함.
- ASC   ; 오름차순 ( Ascending )
- DEXC  ; 내림차순 ( Descending )

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