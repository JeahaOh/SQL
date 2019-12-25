# GROUP  
## GROUP BY
한 테이블 내의 **특정 컬럼을 기준**으로 그룹화 하여 테이블의 행들을 그룹별로 구반해야 한다면,  
GROUP BY를 이용하여 같은 값을 갖는 행끼리 그룹화할 수 있음.
```
  SELECT    `기준 열`, 그룹 함수( 열 이름 )  --  4
  FROM      테이블 이름                   --  1
  [WHERE    조건 식]                     --  2
  GROUP BY  열 이름                      --  3
  [ORDER BY 열 이름 ]                    --  5
```
논리 순서
  1. 테이블 접근.
  2. WHERE 조건에 맞는 데이터를 고름.
  3. 기술될 기준 열을 기준으로 같은 데이터 값끼리 그룹화.
  4. 결과를 출력.
  5. ASC 혹은 DESC로 정렬.
- SELECT 절에 기준 열과 그룹 함수가 같이 지정되면,  
  GROUP BY 절의 기준 열 이름이 반드시 기술되어야 함.  
  ( SELECT 절에 그룹 함수만 기술되고, 열 이름이 기술되지 않으면,  
  GROUP BY 절을 반드시 기술할 필요는 없음. )  
- WHERE 절을 사용하면 행을 그룹으로 묶기 전에 앞서 조건식이 적용됨.
- SELECT 절에 그룹 함수를 사용하지 않아도 GROUP BY 절만으로 사용할 수 있음.
  
```
SELECT
  job_id AS 직무, SUM(salary) 직무별_총급여, AVG(salary) 직무별_평균급여
FROM
  employees
WHERE
  employee_id >= 10
GROUP BY
  job_id
ORDER BY
  직무별_총급여 DESC,
  직무별_평균급여;
```
  
그룹에 대한 그룹
```
SELECT
  job_id AS 대그룹,
  manager_id AS 중그룹,
  SUM(salary) 그루핑_총급여,
  AVG(salary) 그루핑_평균급여
FROM
  employees
WHERE
  employee_id >= 10
GROUP BY
  job_id,
  manager_id
ORDER BY
  그루핑_총급여 DESC,
  그루핑_평균급여;
```
  
## HAVING
연산된 그룹 함수 결과에 조건 적용하기.  
SELECT 절에서 WHERE로 조건을 주어주듯,  
HAVING으로 GROUP BY에서 조건식을 적용할 수 있음.  
```
  SELECT    열 이름, 그룹 함수(열 이름)   -- 5
  FROM      테이블 이름                -- 1
  [WHERE    조건식]                   -- 2
  GROUP BY  열 이름                   -- 3
  [HAVING   조건식]                   -- 4
  [ORDER BY 열 이름]                  -- 6
```  
논리 순서
  1. 테이블 접근.
  2. WHERE 조건식에 맞는 데이터 값을 고름.
  3. 기술된 기준 열을 기준으로 같은 데이터 값끼리 그룹화.
  4. 그룹화된 값에 대해 조건식을 적용.
  5. 결과를 가져옴.
  6. ASC, DESC로 정렬.
  
```
SELECT
  job_id AS 직무,
  SUM(salary) 직무별_총급여,
  AVG(salary) 직무별_평균급여
FROM
  employees
WHERE
  employee_id >= 10
GROUP BY
  job_id
HAVING
  SUM(salary) > 30000
ORDER BY
  직무별_총급여 DESC,
  직무별_평균급여;
```
  
| WHERE | HAVING |
|:-----:|:------:|
| 조건을 사용하여 결과를 제한 | 그룹의 결과를 제한 |
| 테이블에서 특정 조건에 부합하는 자료만을 검색 할 때 사용 | 그룹함수를 적용해서 나온 값 중에서 원하는 조건에 부합하는 자료만 산출할 때 사용 |
| 단순 컬럼 | 그룹함수 |
  
# DQL의 실행 순서 재정리
```
  SELECT            -- 5
  FROM              -- 1
  [WHERE            -- 2
  GROUP BY          -- 3
  [HAVING           -- 4
  [ORDER BY 열 이름]  -- 6
```
  
----
그룹 함수를 GROUP BY와 함께 봐야 할까?
