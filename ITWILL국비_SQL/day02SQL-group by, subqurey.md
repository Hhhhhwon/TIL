# 목차
- [목차](#목차)
  - [오라클 함수(function)](#오라클-함수function)
  - [(예) 통계 관련 함수: count, sum, avg, max, min, variance(분산), stddev(표준편차)](#예-통계-관련-함수-count-sum-avg-max-min-variance분산-stddev표준편차)
  - [그룹별 쿼리](#그룹별-쿼리)
  - [문제 연습](#문제-연습)
  - [서브쿼리(subquery): SQL 문장의 일부로 다른 SQL 문장이 포함되는 것.](#서브쿼리subquery-sql-문장의-일부로-다른-sql-문장이-포함되는-것)
  - [예제 연습](#예제-연습)


## 오라클 함수(function)
1. 단일 행 함수:
   행(row) 하나씩 함수의 아규먼트로 전달되고, 행 마다 하나씩 결과가 리턴되는 함수.
   (예) to_date, to_char, lower, upper, ...
2. 다중 행 함수:
   여러개의 행이 함수의 아규먼트로 전달되고, 하나의 결과가 리턴되는 함수.
   (예) 통계 관련 함수: count, sum, avg, max, min, variance(분산), stddev(표준편차)
---

- 단일 행 함수 예 - 모든 행의 값을 소문자로 바꾸기:
```sql
select ename, lower(ename), job, lower(job)
from emp;
```
```sql
 to_char() 함수: 다른 타입의 값을 문자열로 변환. 날짜 -> 문자열.
select hiredate, to_char(hiredate, 'YYYY/MM/DD HH:MI:SS')
from emp;
```

- nvl(변수, 값): 변수가 null이면 값을 리턴하고, null이 아니면 원래 값을 리턴.
- nvl2(변수, 값1, 값2): 변수가 null이 아니면 값1을 리턴하고, null이면 값2를 리턴.
```sql
select comm, nvl(comm, -1), nvl2(comm, comm, -1) from emp;
```
- 다중 행 함수 예:
- count(컬럼): null이 아닌 행의 개수를 리턴.
```sql
select count(empno), count(mgr), count(comm)
from emp;
```
- select count(*) from emp; -- 테이블의 행의 개수
```sql
-- 통계 함수: 합계, 평균, 최댓값, 최솟값, 분산, 표준편차
select sum(sal), avg(sal), max(sal), min(sal), variance(sal), stddev(sal)
from emp;
```

- 단일행 함수와 다중행 함수는 함께 select할 수 없음!
```sql
-- select sal, sum(sal) from emp;
-- select nvl(sal, 0), sum(sal) from emp;
```

## 그룹별 쿼리
```sql
(예) 부서별 급여 평균, 부서별 인원수
(문법)
  select 컬럼, 함수 호출, ...
  from 테이블
  where 조건식(1)
  group by 그룹별로 묶어줄 변수(컬럼), ...
  having 조건식(2)
  order by 정렬 기준 변수(컬럼), ...;
```
```sql
- 부서별 급여 평균
select deptno, round(avg(sal), 2) as "AVG_SAL"
from emp
group by deptno
order by deptno;
```
## 문제 연습
```sql
-- 모든 문제에서 소수점은 반올림해서 소수점 이하 2자리까지 표시
-- Ex1. 부서별 급여 평균, 표준편차를 부서번호 오름차순으로 출력.
select deptno, 
    round(avg(sal), 2) as "AVG_SAL", 
    round(stddev(sal), 2) as "STD_SAL"
from emp
group by deptno
order by deptno;
```
```sql
-- Ex2. 직무별 직무, 직원수, 급여 최댓값, 최솟값, 평균을 직무 오름차순으로 출력.
select job, count(job), 
    max(sal) as "MAX_SAL", min(sal) as "MIN_SAL", 
    round(avg(sal), 2) as "AVG_SAL"
from emp
group by job
order by job;
```
```sql
-- Ex3. 부서별/직무별로 부서번호, 직무, 직원수, 급여 평균을 검색
--      정렬 순서: (1) 부서번호 (2) 직무
select deptno, job, count(*), round(avg(sal), 2)
from emp
group by deptno, job
order by deptno, job;
```
```sql
-- Ex4. 입사연도별 사원수를 검색. (힌트) to_char(날짜, 포맷) 이용.
select to_char(hiredate, 'YYYY-MM-DD') from emp;
select to_char(hiredate, 'YYYY') from emp;
select to_char(hiredate, 'YYYY') as "YEAR", count(*) as "COUNT"
from emp
group by to_char(hiredate, 'YYYY')
order by YEAR;
-- select 절에서 만든 별명(alias)는 order by 절에서만 사용 가능!
```
```sql
-- where 절은 테이블에서 조건에 맞는 행들을 선택할 때.
-- having 절은 그룹별 쿼리에서 조건에 맞는 그룹을 선택할 때.

-- 부서별 급여 평균 검색. 급여 평균이 2000 이상인 부서만 검색:
select deptno, avg(sal)
from emp
group by deptno
having avg(sal) >= 2000
order by deptno;
```
```sql
-- Ex. mgr 컬럼이 null이 아닌 직원들 중에서 부서별 급여 평균을 검색.
-- 정렬순서: 부서번호 오름차순.
select deptno, round(avg(sal), 2)
from emp
where mgr is not null
group by deptno
order by deptno;

select * from emp where deptno = 10;
```
```sql
-- Ex. 직무별 사원수를 검색. PRESIDENT는 검색 제외. 
-- 직무별 사원수가 3명 이상인 직무만 검색.
-- 정렬순서: 직무의 오름차순.
select job, count(job)
from emp
where job != 'PRESIDENT'
group by job
having count(job) >= 3
order by job;

select job, count(job)
from emp
group by job
having job != 'PRESIDENT' and count(job) >= 3
order by job;
```
```sql
-- Ex. 입사연도, 부서번호, 입사연도별 부서별 사원수 검색
-- 1980년은 검색에서 제외.
-- 연도별 부서별 사원수가 2명 이상인 경우만 선택.
-- (1) 연도별, (2)부서별 오름차순 출력.
select to_char(hiredate, 'YYYY') as "YEAR", deptno, count(*) as "COUNT"
from emp
where to_char(hiredate, 'YYYY') != '1980'
group by to_char(hiredate, 'YYYY'), deptno
having count(*) >= 2
order by YEAR, deptno;

select to_char(hiredate, 'YYYY') as "YEAR", deptno, count(*) as "COUNT"
from emp
group by to_char(hiredate, 'YYYY'), deptno
having to_char(hiredate, 'YYYY') != '1980' and count(*) >= 2
order by YEAR, deptno;
```
---

## 서브쿼리(subquery): SQL 문장의 일부로 다른 SQL 문장이 포함되는 것.

```sql
-- 급여 평균보다 더 많은 급여를 받는 직원들?
select avg(sal) from emp;
select * from emp where sal >= 2073.2;

select * from emp
where sal >= (select avg(sal) from emp);

select ename, sal,
    round(sal - (select avg(sal) from emp), 2) as "DIFF"
from emp;
```
## 예제 연습
```sql
-- ALLEN보다 적은 급여를 받는 직원들의 사번, 이름, 급여를 검색.
-- select * from emp where ename = 'ALLEN';
select empno, ename, sal
from emp
where sal < (
    select sal from emp where ename = 'ALLEN'
);
```
```sql
-- ALLEN과 같은 직무를 갖는 직원들의 사번, 이름, 부서번호, 직무, 급여를 검색.
select empno, ename, deptno, job, sal
from emp
where job = (
    select job from emp where ename = 'ALLEN'
);
```
```sql
-- SALESMAN의 급여 최댓값보다 더 많은 급여를 받는 직원들의 이름, 급여, 직무를 검색.
select ename, sal, job
from emp
where sal > (
    select max(sal) from emp where job = 'SALESMAN'
);
```
```sql
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
```
```sql
-- SCOTT과 같은 급여를  받는 직원들의 이름과 급여를 검색.
select ename, sal
from emp
where sal = (
    select sal from emp where ename = 'SCOTT'
);
```
```sql
-- 위 결과에서 SCOTT은 제외하고 검색.
select ename, sal
from emp
where ename != 'SCOTT'
    and
    sal = (
        select sal from emp where ename = 'SCOTT'
    );
```
```sql
-- ALLEN보다 늦게 입사한 직원들의 이름, 입사날짜를 최근입사일부터 출력.
select ename, hiredate
from emp
where hiredate > (
    select hiredate from emp where ename = 'ALLEN'
)
order by hiredate desc;
```
```sql
-- 매니저가 KING인 직원들의 사번, 이름, 매니저 사번을 검색.
select empno, ename, mgr
from emp
where mgr = (
    select empno from emp where ename = 'KING'
);
```
```sql
-- ACCOUNTING 부서에 일하는 직원들의 이름, 급여, 부서번호를 검색.
select ename, sal, deptno
from emp
where deptno = (
    select deptno from dept where dname = 'ACCOUNTING'
);
```
```sql
-- CHICAGO에서 근무하는 직원들의 이름, 급여, 부서 번호를 검색.
select ename, sal, deptno
from emp
where deptno = (
    select deptno from dept where loc = 'CHICAGO'
);
```
---