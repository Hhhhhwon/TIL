# 목차 
- [목차](#목차)
  - [서브쿼리(subquery): SQL 문장의 일부로 다른 SQL 문장이 포함되는 것](#서브쿼리subquery-sql-문장의-일부로-다른-sql-문장이-포함되는-것)
  - [서브쿼리 문제 풀이](#서브쿼리-문제-풀이)
## 서브쿼리(subquery): SQL 문장의 일부로 다른 SQL 문장이 포함되는 것


## 서브쿼리 문제 풀이
```sql
-- 급여 평균보다 더 많은 급여를 받는 직원들?
select avg(sal) from emp;
select * from emp where sal >= 2073.2;

select * from emp
where sal >= (select avg(sal) from emp);

select ename, sal,
    round(sal - (select avg(sal) from emp), 2) as "DIFF"
from emp;

-- ALLEN보다 적은 급여를 받는 직원들의 사번, 이름, 급여를 검색.
-- select * from emp where ename = 'ALLEN';
select empno, ename, sal
from emp
where sal < (
    select sal from emp where ename = 'ALLEN'
);

-- ALLEN과 같은 직무를 갖는 직원들의 사번, 이름, 부서번호, 직무, 급여를 검색.
select empno, ename, deptno, job, sal
from emp
where job = (
    select job from emp where ename = 'ALLEN'
);

-- SALESMAN의 급여 최댓값보다 더 많은 급여를 받는 직원들의 이름, 급여, 직무를 검색.
select ename, sal, job
from emp
where sal > (
    select max(sal) from emp where job = 'SALESMAN'
);

-- WARD의 연봉보다 더 많은 연봉을 받는 직원들의 이름, 급여, 수당, 연봉을 검색.
-- 연봉 = sal * 12 + comm. comm(수당)이 null인 경우에는 0으로 계산.
-- 정렬 순서: 연봉 내림차순.
select * from emp where ename = 'WARD'; -- WARD 직원의 레코드
select sal * 12 + comm from emp where ename = 'WARD'; -- WARD의 연봉
select sal * 12 + nvl(comm, 0) from emp; -- 모든 직원의 연봉

select ename, sal, comm, sal * 12 + nvl(comm, 0) as "ANNUAL_SAL"
from emp
where sal * 12 + nvl(comm, 0) > (
    select sal * 12 + nvl(comm, 0) from emp
    where ename = 'WARD'
)
order by ANNUAL_SAL desc;

-- SCOTT과 같은 급여를  받는 직원들의 이름과 급여를 검색.
select ename, sal
from emp
where sal = (
    select sal from emp where ename = 'SCOTT'
);

-- 위 결과에서 SCOTT은 제외하고 검색.
select ename, sal
from emp
where ename != 'SCOTT'
    and
    sal = (
        select sal from emp where ename = 'SCOTT'
    );

-- ALLEN보다 늦게 입사한 직원들의 이름, 입사날짜를 최근입사일부터 출력.
select ename, hiredate
from emp
where hiredate > (
    select hiredate from emp where ename = 'ALLEN'
)
order by hiredate desc;

-- 매니저가 KING인 직원들의 사번, 이름, 매니저 사번을 검색.
select empno, ename, mgr
from emp
where mgr = (
    select empno from emp where ename = 'KING'
);

-- ACCOUNTING 부서에 일하는 직원들의 이름, 급여, 부서번호를 검색.
select ename, sal, deptno
from emp
where deptno = (
    select deptno from dept where dname = 'ACCOUNTING'
);

-- CHICAGO에서 근무하는 직원들의 이름, 급여, 부서 번호를 검색.
select ename, sal, deptno
from emp
where deptno = (
    select deptno from dept where loc = 'CHICAGO'
);

-- 단일 행 서브쿼리: 서브쿼리의 결과 행이 1개 이하인 경우.
-- 단일 행 서브쿼리는 단순 비교(=, !=, >, >=, <. <=)를 할 수 있음.
-- 다중행 서브쿼리: 서브쿼리의 결과 행이 2개 이상인 경우.
-- 다중행 서브쿼리는 단순 비교를 할 수 없음!
-- 다중행 서브쿼리에서는 in, any, all과 같은 키워드를 함께 사용.

-- 각 부서에서 급여를 가장 많이 받는 직원의 레코드(모든 컬럼) 검색:
SELECT * FROM emp
WHERE (deptno, sal) in (
    SELECT deptno, max(sal) FROM emp GROUP BY deptno
);

-- 각 부서에서 급여를 가장 적은 직원의 레코드(모든 컬럼) 검색:
SELECT * FROM emp
WHERE (deptno, sal) in (
    SELECT deptno, MIN(sal) FROM emp GROUP BY deptno
);

-- 다중행 서브쿼리에서 any vs all:
-- (1) any: 여러개 중에서 적어도 하나.
-- (2) all: 여러개 모두(전부).
SELECT * FROM emp
WHERE sal < any (
    SELECT sal FROM emp WHERE deptno = 10
);

SELECT * FROM emp
WHERE sal < all (
    SELECT sal FROM emp WHERE deptno = 10
);

SELECT * FROM emp
WHERE sal = any (
    SELECT sal FROM emp WHERE deptno = 10
);
```