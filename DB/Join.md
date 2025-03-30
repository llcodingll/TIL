## Join


: 둘 이상의 테이블에서 데이터를 조회하기 위해 사용
- 조인 조건은 일반적으로 PK, FK로 구성
    - PK, FK 관계 없이도 논리적 연관만으로도 join 가능
- 종류
- INNER JOIN(= EQUI JOIN)
  - 조인 조건에 해당하는 컬럼 값이 양쪽 테이블에 모두 존재하는 경우에만!
  - N개의 테이블 조인 시, N-1개의 조인 조건 필요
- OUTER JOIN
  - 조인 조건에 해당하는 칼럼 값이 한 쪽 데이블에만 존재해도 조회 기준 데이블에 따라 아래와 같이 나뉨
    - LEFT OUTER JOIN
    - RIGHT OUTER JOIN

---
### Cartesian Product(카타시안 곱)
- 조인 조건 지정 X
- 조인 조건 부적합
```sql
select empno, ename, job, d.deptno, d.dname from emp e, dept d where e.deptno = d.deptno;
```

### 조인 필요성
여러 번 쓸 거 한 번만 쓰자
```sql
select ename, job, deptno from emp where empno = 7788;
select dname from dept where deptno = 20;
select empno, ename, job, e.deptno, dname from emp e, dept d where e.deptno = d.deptno and empno = 7788;
```
---
### INNER JOIN


: 두 테이블에서 일치하는 값을 가진 record 조회

```sql
-- INNER JOIN 키워드 사용해보자.
select empno, ename, job, e.deptno, dname, loc from emp e INNER JOIN dept d ON e.deptno = d.deptno where empno = 7788;

-- USING : 같은 거, 이름 다르게 되어있으면 쓸 일 없겠지요
select ename, job, deptno, dname from emp INNER JOIN dept USING (deptno) where empno = 7788;

```
---
### OUTER JOIN


: 두 테이블에서 하나의 테이블에 조인 조건 데이터가 `존재하지 않아도` 데이터를 조회하기 위함

* 기준이 되는 테이블에 따라 LEFT OUTER, RIGHT OUTER JOIN으로 구분

- **LEFT OUTER JOIN**

    ```sql
    -- 부서 없는 직원 1명 고용
    insert into emp values (7777, '바밤바', 'PRODUCT', 7839, '2025-03-19', 8000, NULL, NULL);
    select ename, e.deptno, d.dname from emp e, dept d where e.deptno = d.deptno; -- 부서 없으니까 바밤바는 아직 조회가 안 됨
    -- 그래서 부서가 없다고 null 넣는 게 아니라 통계할 때처럼 **결측값 설정**해주는 게 나중에 조회할 일 생기면 좋겠지
    ```

- **RIGHT OUTER JOIN**

    ```sql
    -- 한쪽 테이블에 기준을 두고 쓰기
    -- emp 테이블 기준 : emp 테이블에 해당하는 모든 데이터 출력하고 dept에 있는 게 붙을 수 있으면 같이 나온다 = 바밤바 등장
    select ename, e.deptno, d.dname from emp e LEFT OUTER JOIN dept d ON e.deptno = d.deptno;
    -- dept 테이블 기준: dept 테이블에 해당하는 모든 데이터 + emp에서 해당되는 거 붙음 = 바밤바 등장 X
    select ename, d.deptno, d.dname from emp e RIGHT OUTER JOIN dept d ON e.deptno = d.deptno;
    ```
---
### SELF JOIN


: 같은 데이블 2개 조인

```sql
-- 셀프 조인
-- 모든 사원의 이름, 매니저 번호, 매니저 이름
select e1.empno, e1.ename, e2.empno, e2.ename from emp e1, emp e2 where e1.mgr = e2.empno;

-- King없어..ㅠ
select e1.empno, e1.ename, e2.empno, e2.ename from emp e1 LEFT OUTER JOIN emp e2 ON e1.mgr = e2.empno;
```
---
### Non-Equi JOIN


: 조인 조건이 PK, FK로 정확히 일치하는 게 아닐 때 사용

```sql
-- 비 동등 조인(Non-Equi JOIN)

-- 모든 사원의 사번, 이름, 급여, 급여 등급 조회
select e.empno, e.ename, e.sal, sg.grade from emp e, salgrade sg where e.sal between sg.losal and sg.hisal order by sg.grade desc, e.sal desc;
```
---
## SubQuery


: SQL문 안에 포함되어 있는 SQL문

- outer query(= main query)
- inner query

### 서브 쿼리 종류

- 중첩 서브 쿼리(Nested query) - WHERE절
- 인라인 뷰 - FROM절
- 스칼라 서브 쿼리  - SELECT절

### 서브 쿼리 포함할 수 있는 SQL문

- SELECT, FROM, WHERE, HAVING, ORDER BY
- INSERT문의 VALUES
- UPDATE문의 SET

### 서브 쿼리 사용 시, 주의사항

- 반드시 `()`로 감싸서 사용
- 단일 행 || 다중 행 비교 연산자와 함께 사용 가능
    - 단일 행 비교 연산자는 서브 쿼리 결과가 1건 이하
    - 복수 행 비교 연산자는 결과 건수와 상관 x

### 서브 쿼리 필요성

INNER JOIN 수행하는 경우, 쿼리 복잡하고 카타시안 곱으로 인해 속도 느려짐

JOIN 복잡한데 걍 없이 ㄱㄱㄱ하는 거

```sql
# 1. 매니저의 이름이 KING인 사원의 사번, 이름, 부서번호, 업무 
select empno, ename, deptno, job from emp where mgr = (select empno from emp where ename = 'KING');
# 2. 7566번 사원보다 급여를 많이 받는 사원의 이름, 급여를 조회
select ename, sal from emp where sal > (select sal from emp where empno = 7566);
# 3. 20번 부서의 평균 급여보다 급여가 많은 사원의 사번, 이름, 업무, 급여조회
select empno, ename, job, sal from emp where sal > (select avg(sal) from emp where deptno = 20);
# 4. 업무가 TURNER와 같고/ 사번 7934인 직원보다 급여/가 많은 사원의 사번, 이름, 업무를 조회
select empno, ename, job from emp where job = (select job from emp where ename = 'TURNER') and sal > (select sal from emp where empno = 7934);
```
---
### 다중 행 IN / ANY / ALL

```sql
# 5. 업무가 SALESMAN 인 직원들 중 최소 한명 이상보다 많은 급여를 받는 사원의 이름, 급여, 업무를 조회하시오.
# > ANY : 최소값보다는 큰
# < ANY : 최대값보다는 작은
select ename, sal, job from emp where sal > ANY (select sal from emp where job = 'SALESMAN');

# 6. 업무가 'SALESMAN'인 모든 직원보다 급여(커미션포함)를 많이 받는 사원의 이름, 급여, 업무, 입사일, 부서번호를 조회하시오.
# > ALL : 최대값보다 큰
# < ALL : 최소값보다 작은
select ename, sal, job, hiredate, deptno from emp where sal > (select sal+ifnull(comm, 0) from emp where job = 'SALESMAN') and job != 'SALESMAN';

# 7. 직원이 최소 한명이라도 근무하는 부서의 부서번호, 부서이름, 위치
# IN : 다중행에 하나라도 일치하면 조회 (= ANY 와 동일)
select deptno, dname, loc from dept where deptno in (select distinct deptno from emp);
```
---
### Nested Subquery 다중 열

```sql
# 다중 열
# 8. 이름이 FORD인 사원과 매니저 및 부서가 같은 사원의 이름, 매니저번호, 부서번호를 조회 
select ename, mgr, deptno from emp where (mgr, deptno) = (select mgr, deptno from emp where ename = 'FORD') and ename <> 'FORD';

# 9. 각 부서별 / 입사일이 가장 빠른 / 사원의 사번, 이름, 부서번호, 입사일을 조회
select empno, ename, deptno, hiredate from emp where (deptno, hiredate) in (select deptno, min(hiredate) from emp group by deptno);
```
---
### Correlated Subqueries 상호 연관 서브 쿼리


: 외부 쿼리에 있는 테이블에 대한 참조를 하는 서브 쿼리
- FROM절에는 t1에 대한 선언 존재 X ⇒ 외부 쿼리(메인 쿼리)에서 t1을 참조
- 행을 먼저 읽어 각 행의 값을 관련된 데이터와 비교하는 방법 중 하나
- 서브 쿼리에서는 메인 쿼리 컬럼명 사용 가능한데 반대는 불가

```sql
# 10. 소속 부서의 평균 급여보다 많은 급여를 받는 사원의 이름, 급여, 부서번호, 입사일, 업무를 조회
select ename, sal, deptno, hiredate, job from emp e where sal > (select avg(sal) from emp where deptno = e.deptno);
```
---
### Inline View


: 임시적인 테이블 하나 만들어서 자주 쓰는 결과들을 view라는 이름으로 저장
- FROM절에서 사용
- 동적으로 생성된 테이블로 사용 가능, View와 같은 역할
  from절에 있는 서브쿼리 날려서 하나의 테이블처럼 이용 가능
- SQL문이 실행될 때만 임시적으로 생성되는 뷰

```sql
# 11. 모든 사원의 평균급여보다 적게 받는 사원들과 같은 부서에서 근무하는 사원의 사번, 이름, 급여, 부서번호를 조회
select e.empno, e.ename, e.sal, e.deptno from emp e, (select distinct deptno from emp where sal < (select avg(sal) from emp)) d where e.deptno = d.deptno;
```
---
### Scalar Subquery


: 하나의 행에서 하나의 컬럼 값만 반환

- 사용 가능한 경우
    - GROUP BY 제외한 SELECT의 모든 절
    - INSERT 문의 VALUES
    - 조건 및 표현식 부분
    - UPDATE문의 SET 또는 WHERE절에서 연산자 목록

```sql
# 12. 모든 사원에 대하여 사원의 이름, 부서번호, 급여, 사원이 소속된 부서의 평균 급여를 조회 (단, 이름 오름차순)
select ename, deptno, sal, (select avg(sal) from emp where deptno = e.deptno) as avgsal from emp e;

# 13. 사원의 이름, 부서번호, 급여, 소속부서의 평균 급여를 조회
select ename, deptno, sal, (select avg(sal) from emp where deptno = e.deptno) as avgsal from emp e;

# 14. 부서번호가 10인 부서의 총 급여, 20인 부서의 평균 급여, 30인 부서의 최고, 최저 급여
select (select sum(sal) from emp where deptno = 10) sum10,
(select avg(sal) from emp where deptno = 20) avg20,
(select max(sal) from emp where deptno = 30) max30,
(select min(sal) from emp where deptno = 30) min30;

# 15. 모든사원의 번호, 이름, 부서번호, 입사일을 조회 (단, 부서이름기준으로 내림차순)
update emp set deptno = 40 where ename = 'SSAFY';
select empno, ename, deptno, hiredate from emp e order by (select dname from dept where deptno = e.deptno) desc;
```
---
### Subquery

```sql
create table emp_copy (select * from emp);
create table emp_blank (select * from emp where 1 = 0);
insert into emp_blank (select * from emp where deptno = 30);
```