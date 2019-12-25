# FUNCTION
DB에서 제공하는 미리 정의 된 기능.  
- 데이터 값을 계산하거나 조작.      (단일 행 함수)
- 열의 데이터 타입을 변환.
- 행의 그룹에 대해 계산하거나 요약.  (그룹 함수)
  
## DUAL 테이블
쿼리문의 수행 결과가 하나의 ROW로 출력되기 위한 DUMMY 컬럼만 갖고 있음.  
함수를 위한 임시 테이블 같은 개념.  
  
# 단일 행 함수 : 데이터 값을 계산 혹은 조작
- 각 행에 대해 수행.
- 데이터 타입에 맞는 함수를 사용 해야 함.
- 행렬로 하나의 결과를 반환.
- SELECT, WHERE, ORDER BY 절 등에서 사용 가능.
- 함수 속의 함수로 중첩해서 사용 가능.
  
단일 행 함수의 종류.  
| 종류     | DESC                                     |
|--------:|:-----------------------------------------|
| 문자 타입 | 문자를 입력받아 문자와 숫자를 반환.              |
| 숫자 타입 | 숫자를 입력받아 숫자를 반환.                    |
| 날짜 타입 | 날짜 연산, 날짜 값 반환.                      |
| 변환 타입 | 임의의 데이터 타입의 값을 다른 데이터 타입으로 변환.  |
| 일반 함수 | NVL, DECODE, CASE, WHEN, 순위 함수 등.      |


## 문자 처리 함수
|   |   |   |
|---|---|---|
|  lower                 |  소문자 반환                  |  lower('fuck DB') = 'fuck db'  |
|  upper                 |  대문자 반환                  |  upper('fuck DB') = 'FUCK DB'  |
|  initcap               |  문자열의 첫글자 대문자, 나머지 소문자  |  initcap('fuck DB') = 'Fuck Db'  |
|  substr                |  문자를 잘라 추출 (한글1byte)   |  substr('Welcome to Oracle',4,3) = 'com' substr('Welcome to Oracle',-4,3) = 'acl' |
|  substrb               |  문자를 잘라 추출 (한글 2byte)  |  substr('웰컴투오라클',3,4) = 투오라클, substrb('웰컴투오라클’,3,4) = 컴투 |
|  concat                |  문자의 값을 연결              | CONCAT('fuck', ' DB')  |
|  length                |  문자의 길이 반환 (한글 1byte)  |  length('오라클’) = 3  |
|  lengthb               |  문자의 길이 반환 (한글 2byte)  |  lengthb('오라클’) = 6 |
|  lpad / rpad           |  입력 받은 문자열과 기호를 정렬하여 특정 길이의 문자열로 반환  |  "lpad('oracle',10,'#') = '####oracle'" |
|  trim / ltrim / rtrim  |  잘라내고 남은 문자 표시         |  rtrim('  oracle  ') = '  oracle'trim('a' from 'aaaORACLEaaa') = 'ORACLE' |
|  convert               |  char set으로 변환            |    |
|  chr                   |  ascii 코드 값으로 변환         |    |
|  ascii                 |  ascii 코드값을 문자로 반환      |  ascii('Oracle')  |
|  replace               |  문자열에서 특정문자 변경         |    |
|  instr                 |  특정 문자의 위치 반환           |  instr('Welcome to Oracle', 'o') = 5instr(대상,찾을글자,시작위치,몇번째발견)  |

## 숫자 처리 함수
|   |   |   |
|---|---|---|
|  round  |  특정 자릿수에서 반올림.   ( -시 정수값도 가능)  |  round(대상,(-)자릿수)  |
|  trunc  |  특정 자릿수에서 버림, 절단.( -시 정수값도 가능)  |  trunc(대상,(-)자릿수)  |
|  ceil  |  올림  |    |
|  floor  |  버림  |    |
|  ''  |  ''  |  ''  |
|  abs  |  절대값 반환  |    |
|  cos  |  cosine  |    |
|  exp  |  e의 n승  |    |
|  floor  |  소수점 아래를 자름 (버림)  |    |
|  log  |  log값 반환  |    |
|  power  |  power(man) m의 n승 반환  |    |
|  sign  |  sign(n) n<0이면 -1  |   n=0이면 0,n>0이면 1  |    |
|  sin  |  sine값 반환  |    |
|  tan  |  tangent값 반환  |    |
|  mod  |  입력 받은 수를 나눈 나머지값 반환.  |  mod(대상,2) = 1 (java 에서 %)  |


## 날짜 처리 함수

### 날짜 연산
|    날짜  연산        |  DESC            |  반환값  |
|---|---|---|
| Date + Number      | 날짜에 일수를 더한다. |  Date  |
| Date - Number      | 날짜에 일수를 뺀다.  |  Date  |
| Date - Date        | 날짜에서 날짜를 뺀다. |  일 수  |
| Date + Number / 24 | 날짜에 시간을 더할 때는 시간을 24로 나누어서 날짜에 더한다.| Date |

```
SELECT
  TO_CHAR( SYSDATE, 'YY/MM/DD/HH24:MI' ),
  SYSDATE + 1,
  SYSDATE - 1,
  (SYSDATE + 1) - (SYSDATE - 7),
  SYSDATE + 13 / 24
FROM
  DUAL;
```

### 날짜 처리 함수
MONTH_BETWEEN 함수 외에는 모두 날짜 타입을 반환함.

|   |   |   |
|---|---|---|
|  sysdate  |  시스템상 현재 날짜 반환  |  sysdate+1 = 내일날짜  |
|  months_between  |  두 날짜 사이가 몇 개월인지 반환  |  between(date1, date2)  |
|  add_months  |  특정 날짜에 개월수 더함  |  add_months(date, number)  |
|  next_day  |  특정 날짜에서 최초 요일의 날짜 반환  |  next_day(date, 요일)sysdate, next_day(sysdate, '수')09.01.17, 09.01.21  |
|  last_day  |  해당 달의 마지막달 반환  |  last_day(sysdate) = 18.07.31  |
|  round  |  인자로 받은 날짜를 특정 기준으로 반올림  |  round(date, format)round(hiredate, month) = day < 16 = 이달.01, day > 16 = 담달.01  |
|  trunc  |  인자로 받은 날짜를 특정 기준으로 버림  |  trunc(date, format)  |

#### MONTHS_BETWEEN
두 날짜 사이의 개월 수 계산
```
  MONTHS_BETWEEN( 날짜, 날짜 )
```
```
SELECT
  SYSDATE, hire_date, MONTHS_BETWEEN( SYSDATE, hire_date )
FROM
  employees
WHERE
  department_id = 100;
```
#### ADD_MONTHS
월에 날짜 더하기
```
  ADD_MONTHS( 날짜, 숫자 )
```
```
SELECT
  hire_date,
  ADD_MONTHS( hire_date, 3),
  ADD_MONTHS( hire_date, -3)
FROM
  employees
WHERE
  department_id BETWEEN 100 AND 106; 
```
### NEXT_DAY
돌아오는 요일의 날짜 개산하기
```
  NEXT_DAY( 날자, '요일' or 숫자 )
```
```
SELECT
  hire_date,
  NEXT_DAY( hire_date, 'Friday'),
  NEXT_DAY( hire_date, 6)
FROM
  employees
WHERE
  department_id BETWEEN 100 AND 106; 
```
### LAST_DAY
돌아오는 월의 마지막 날짜 계산하기
```
  LAST_DAY( 날짜 )
```
```
SELECT
  hire_date,
  LAST_DAY( hire_date )
FROM
  employees
WHERE
  department_id BETWEEN 100 AND 106; 
```
### ROUND, TRUNC
날짜를 반올림 혹은 절삭
```
  ROUND or TRUNC ( 날짜, 지정 값[MONTH, YEAR등] )
```
```
SELECT
  hire_date,
  ROUND( hire_date, 'MONTH' ),
  ROUND( hire_date, 'YEAR' ),
  TRUNC( hire_date, 'MONTH' ),
  TRUNC( hire_date, 'YEAR' )
FROM
  employees
WHERE
  department_id BETWEEN 100 AND 106; 
```

## 형 변환 함수
### TO_DATE
날짜를 나타내는 문자열을 명시도니 날짜 형식으로 변환하는 함수
```
  TO_DATE( 문자열, '지정형식' )
```
```
SELECT
  TO_DATE( '20111217', 'YYYYMMDD')
FROM
  DUAL;
```
### TO_NUMBER
숫자 타입의 문자열을 숫자 데이터 타입으로 변환하는 함수. 데이터 타입만 바뀜.
```
  TO_NUMBER( '숫자' )
```
```
SELECT
  TO_NUMBER('1234')
FROM
  DUAL;
```

### TO_CHAR
숫자 값을 지정한 데이터 형식의 문자열로 변환
```
  TO_CHAR( 숫자 데이터 타입, '지정 형식' )
```
  
| 지정 형식 | DESC | EX | RESULT |
|:-------:|:----:|:---:|:----:|
|   9   |  9로 출력 자릿수 지정  |  TO_CHAR( 42000, '99999999' )  |  '   42000'  |
|   0   |  자릿수 만큼 0을 출력  |  TO_CHAR( 42000, '09999999' )  |  00042000  |
|   $   |  달러               |  TO_CHAR( 42000, '$9999999' )  |  $42000    |
|   L   |  지역 화폐 기호       |  TO_CHAR( 42000, 'L9999999' )  |  $42000    |
ㅣ  `,`  |  명시한 위치에 쉼표    |  TO_CHAR( 42000, '9,999,999' ) |  43,000    |
|  `.`  |  명시한 위치에 소수점  |  TO_CHAR( 42000, '9999999.99' ) |  42000.00  |

### TO_CHAR
날자 값을 지정한 형식의 문자열 타입으로 면환
```
  TO_CHAR( 날짜 데이터 타입, '지정 형식' )
```
  
| 지정 형식 | DESC |
|:-------:|:----:|
|   CC    | 세기          |
|   YY    | 연도          |
|   YEAR  | 문자 연도      |
|   Q     | 분기          |
|   MM    | 숫자값 월      |
|  MONTH  | 문자값 월      |
|   MON   | 문자값 약어 월  |
|   RM    | 로마자 월      |
|   W     | 년월의 주      |
|   DD    | 년월주의 일    |
|   DAY   | 요일이름       |
|   DY    | 요일 이름 약어  |

## 일반 함수
### NVL
```
  NVL( 열이름, '치환 값' )
```
NULL 값을 치환 값으로 처리함.
```
SELECT
  salary * NVL( commission_pct, 1 )
FROM
  employees
ORDER BY
  commission_pct;
```

### NVL2
```
  NVL2( COLUMN1, COLUMN2, COLUMN3 )
```
COLUMN1의 값이 NULL이면 COLUMN3를 출력 NULL이라면 COLUMN2를 출력.

### DECODE
조건 논리 처리.  
3항 연산과 같음.
```
  DECODE( 열 이름, 조건 값, 치환 값, 기본 값 )
```
```
SELECT
  first_name,
  last_name,
  department_id,
  salary as 급여,
  DECODE( department_id, 60, salary * 1.1, salary )   as 조정급여,
  DECODE( department_id, 60, '10%인상', '미인상' )    as 인상여부
FROM
  employees;
ORDER BY
  commission_pct;
```

### CASE
복잡한 조건 논리처리 하기
```
CASE
  WHEN  조건 1  THEN  출력 값 1
  WHEN  조건 3  THEN  출력 값 2
  ...
  ELSE  출력 값 3
END
```
```
SELECT
  employee_id, first_name, last_name, salary,
  CASE
    WHEN salary >= 9000 THEN 'TOP'
    WHEN salary BETWEEN 6000 AND 8999 THEN 'MID'
    ELSE 'LOW'
  END AS salary_grade
FROM
  employees
WHERE
  job_id = 'IT_PROG';

```

### RANK, DENSE_RANK, ROW_NUMBER
데이터 값에 순위 매기기
|  FUNC  |  DESC  |  EX  |
|--------|--------|------|
|  RANK  |  공동 순위를 출력하되, 공동 순위만큼 건너 뛰어 다음 순위 출력.  | 1, 2, 2, 4, ... |
|  RANK  |  공동 순위를 출력하되, 건너 뛰지 않고 이어서 다음 순위 출력.   | 1, 2, 2, 3, ... |
|  RANK  |  공동 순위없이 순위 출력.                              | 1, 2, 3, 4, ... |

```
  RANK () OVER ( [PARTITION BY 열 이름] ORDER BY 열 이름)
```
```
SELECT
  employee_id, salary,
  RANK()       OVER( ORDER BY salary DESC ) AS RANK_SALARY,
  DENSE_RANK() OVER( ORDER BY salary DESC ) AS DENSE_RANK_SALARY,
  ROW_NUMBER() OVER( ORDER BY salary DESC ) AS ROW_NUMBER_SALARY
FROM
  employees;
```
```
SELECT
  A.employee_id, A.department_id, B.department_name, A.salary,
  RANK()       OVER( PARTITION BY A.department_id ORDER BY salary DESC ) AS RANK_SALARY,
  DENSE_RANK() OVER( PARTITION BY A.department_id ORDER BY salary DESC ) AS DENSE_RANK_SALARY,
  ROW_NUMBER() OVER( PARTITION BY A.department_id ORDER BY salary DESC ) AS ROW_NUMBER_SALARY
FROM
  employees A, departments B
WHERE
  A.department_id = B.department_id
ORDER BY B.department_id, A.salary DESC;
```

## 그룹 함수
집계 함수라고도 함.  
단일 행 함수와 달리 여러 행에 대해 함수가 적용되어 하나의 결과를 나타내는 함수.  
기준 열에 대해 같은 데이터 값 기리 그룹으로 묶고,  
묶은 행의 집합에 대해 그룹 함수 연산이 필요하다면 GROUP BY 절을 이용하여 처리할 수 있음.  
묶은 그룹에 대해 조건이 필요하다면 HAVING 절을 이용함.

### 그룹 함수의 사용법
```
  SELECT  그룹함수( 열 이름 )
  FROM    테이블 이름
  [WHERE 조건식]
  [ORDER BY 열 이름]
```

### 주요 그룹 함수
  예제 생략
|  FUNC |  DESC          |  EX    |    |
|-------|----------------|--------|----|
| count |  행 개수를 셈     |  count(comm)  |  NULL값도 셈|
|  sum  |  합계           |  sum(comm)  |    |
|  avg  |  그룹의 평균      |  avg(salary)  |  |
|  max  |  그룹의 최댓값  |  max(salary)  |  |
|  min  |  그룹의 최소값  |  min(salary)  |  |
|  stddev  |  그룹의 표준편차  |    |  |
|  variance  |  그룹의 분산  |    |  |

### GROUP BY
특정 열의 데이터 값을 기준으로 그룹화 하여 다른 열에 그룹 함수를 적용해야 한다면?  
GROUP BY를 이용하여 같은 값을 갖는 행끼리 그룹화할 수 있음.
```
  SELECT    기준 열, 그룹 함수( 열 이름 )   --  4
  FROM      테이블 이름                   --  1
  [WHERE    조건 식]                    --  2
  GROUP BY  열 이름                      --  3
  [ORDER BY 열 이름]                    --  5
```
논리 순서
  1. 테이블 접근.
  2. WHERE 조건에 맞는 데이터를 고름.
  3. 기술될 기준 열을 기준으로 같은 데이터 값끼리 그룹화.
  4. 결과를 출력.
  5. ASC 혹은 DESC로 정렬.