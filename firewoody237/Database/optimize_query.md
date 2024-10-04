# 쿼리 최적화
## 1. 좌변을 연산하지 않을 것

```
-- 예시
WHERE YEAR(date) = 2021;
```

- 좌변의 데이터 원본을 변형하면, 인덱스를 활용할 수 없음
    - 인덱스는 원본 데이터를 그대로 사용하여 구성
- 결국엔 모든 데이터를 훑는 상황이 발생

### 대안 : 우변에서의 데이터 필터링
- 데이터를 변형하지 않고, 원본을 유지하며 쿼리
```
WHERE date >= '2021-01-01' AND date <= '2021-12-31';
```

## 2. OR 대신 UNION을 사용할 것
```
-- 예시
WHERE department = 'Marketing' OR department = 'IT';
```

- `OR` 조건은 한 번의 스캔으로 모든 조건을 확인해야 하기 때문에, 불필요한 데이터까지 대량으로 검색
- 인덱스를 제대로 활용하지 못하는 경우도 많음
    - 인덱스는 단일 값에 대한 빠른 검색을 위해 최적화 되어있는데, `OR` 은 여러 값을 동시에 찾아야 함
- 인덱스가 없더라도, 논리적 연산이 추가되어 성능은 낮아짐

### 대안 : UNION 사용
```
WHERE department = 'Marketing'
UNION
WHERE department = 'IT';
```
- `UNION` 을 통해 각 쿼리를 독립적으로 최적화하고 실행

## 3. 필요한 Row와 Column만 선택하여 성능 최적화하기
- `WHERE` 조건으로 불필요한 Row를 줄이는 것이 성능에 유리
- 네트워크 부하의 감소 효과도 볼 수 있음
- 필요한 Column만 선택하는 것이 데이터베이스가 처리해야 할 데이터의 양을 최소화 함으로써 성능에 유리
```
SELECT name, email
FROM employees
WHERE department = 'Marketing' AND sales >= 100000;
```
- 서브쿼리를 활용하여 필요한 데이터만 추출하면, 성능에 유리
    - 서브쿼리를 통해 중간 결과의 크기를 최소화할 수 있기 때문

```
SELECT e.name, e.department, e.sales
FROM employees e
JOIN (
  SELECT department, MAX(sales) AS max_sales
  FROM employees
  GROUP BY department
) d ON e.department = d.department AND e.sales = d.max_sales;
```
- `LIMIT` 키워드를 통해 행의 수를 제한하여 리소스를 절약할 수 있음
```
SELECT name FROM customers LIMIT 50;
```

## 4. 분석 함수를 활용하여 쿼리 성능 높이기
- 대표적으로 `ROW_NUMBER()` , `RANK()` , `DENSE_RANK()` , `LEAD()` , `LAG()`  등이 존재
- 복잡한 데이터 집합 내에서 각 Row별로 세부적인 계산을 가능하게 함
- 집계 함수와 달리 사전에 데이터를 그룹화 할 필요가 없음
- 중간 결과물의 저장과 재처리를 최소화할 수 있음

### 순위 결정 함수로 데이터 순서 매기기
```
SELECT 
  name, 
  department, 
  salary,
  ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rank
  -- 부서별로 급여가 높은 순서대로 랭크
FROM employees;
```

### 데이터 변화를 추적하는 분석 함수
```
SELECT
  name,
  salary,
  LAG(salary) OVER (PARTITION BY department ORDER BY hire_date) AS prev_salary,
  -- 이전 행의 직원 급여를 가져 옴
  salary - LAG(salary) OVER (PARTITION BY department ORDER BY hire_date) AS salary_increase
  -- 급여 인상액
FROM employees;
```

### 분석 함수로 데이터 필터링 최적화하기
```
WITH ranked_employees AS (
  SELECT 
    name, 
    department, 
    salary,
    ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rank
  FROM employees
)
SELECT *
FROM ranked_employees
WHERE rank <= 3;
```

## 5. 와일드카드(%)는 끝에 작성하는 것이 더 좋다
```
SELECT * FROM users WHERE name LIKE '%John';
```

- 와일드 카드를 앞에 쓰면, 데이터베이스가 `John` 으로 끝나는 모든 문자열 조합을 일일이 검색해야 함
- 문자열의 시작 부분을 모르는 경우 인덱스를 활용할 수 없음
    - 일반적으로 인덱스는 사전 순서로 정렬되어 있음
    - 결과적으로 `Index Full Scan` 

```
SELECT * FROM users WHERE name LIKE 'John%';
```
- 데이터베이스가 인덱스를 활용해서 검색 범위를 좁힐 수 있음
    - 인덱스에서 `John` 으로 시작하는 값들을 찾음
    - 인덱스는 사전 순서로 되어있기 때문에 `John` 부분만 찾으면 됨

## 6. 계산값을 미리 정해두었다가, 나중에 조회할 것
- 복잡한 계산을 실시간으로 처리하는 것은 성능에 큰 부담을 줌
- 일단 자주 사용되는 계산 값을 미리 저장해 두었다가, 필요할 때 바로 꺼내 쓰는 것이 효과적

```
SELECT 
    p.product_id,
    AVG(od.quantity * od.unit_price) AS avg_order_amount,
    SUM(od.quantity * od.unit_price) AS total_sales,
    COUNT(DISTINCT o.customer_id) AS num_purchasers,
    COUNT(DISTINCT CASE WHEN o.customer_id IN (
        SELECT customer_id 
        FROM orders
        WHERE product_id = p.product_id
        GROUP BY customer_id
        HAVING COUNT(*) > 1
    ) THEN o.customer_id END) * 1.0 / COUNT(DISTINCT o.customer_id) AS repurchase_rate
FROM 
    products p
    JOIN order_details od ON p.product_id = od.product_id
    JOIN orders o ON od.order_id = o.order_id
GROUP BY 
    p.product_id;
```

```
CREATE TABLE product_stats AS
SELECT
    p.product_id,
    AVG(od.quantity * od.unit_price) AS avg_order_amount,
    SUM(od.quantity * od.unit_price) AS total_sales,
    COUNT(DISTINCT o.customer_id) AS num_purchasers,
    COUNT(DISTINCT CASE WHEN o.customer_id IN (
        SELECT customer_id
        FROM orders
        WHERE product_id = p.product_id
        GROUP BY customer_id
        HAVING COUNT(*) > 1
    ) THEN o.customer_id END) * 1.0 / COUNT(DISTINCT o.customer_id) AS repurchase_rate
FROM
    products p
    JOIN order_details od ON p.product_id = od.product_id
    JOIN orders o ON od.order_id = o.order_id
GROUP BY
    p.product_id;
```

## 7. 가급적이면 `SELECT DISTINCT`  피하기
- 중복된 값의 제거를 위한 `DISTINCT` 는 많은 성능저하를 일으킴
- 메모리 부담

```
SELECT DISTINCT name, age FROM customers;
```

- 고유한 결과를 얻기 위해 충분한 컬럼을 사용하거나, `GROUP BY` 절을 활용

```
SELECT name,age FROM customers GROUP BY name,age;
```

## 그 외

- 인덱스 확인하여, 인덱스 활용하기
- 적절한 `JOIN`  사용하기
- 서브쿼리 최소화하기
- 쿼리 실행 계획 확인하기
- 쿼리 성능 모니터링하기

## 참고 사이트

- [블로그1](https://community.heartcount.io/ko/query-optimization-tips/ "https://community.heartcount.io/ko/query-optimization-tips/")
- [블로그2](https://jhlee-developer.tistory.com/entry/MYSQL-SQL-%EC%BF%BC%EB%A6%AC%EB%AC%B8-%EC%B5%9C%EC%A0%81%ED%99%94-%ED%9A%A8%EC%9C%A8%EC%A0%81%EC%9D%B8-%EC%BF%BC%EB%A6%AC%EB%A5%BC-%EC%9C%84%ED%95%9C-%ED%8C%81 "https://jhlee-developer.tistory.com/entry/MYSQL-SQL-%EC%BF%BC%EB%A6%AC%EB%AC%B8-%EC%B5%9C%EC%A0%81%ED%99%94-%ED%9A%A8%EC%9C%A8%EC%A0%81%EC%9D%B8-%EC%BF%BC%EB%A6%AC%EB%A5%BC-%EC%9C%84%ED%95%9C-%ED%8C%81")
- [블로그3](https://chung-develop.tistory.com/145 "https://chung-develop.tistory.com/145")