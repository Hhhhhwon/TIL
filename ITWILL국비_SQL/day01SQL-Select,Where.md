 # 목차

  * [블록 주석](#블록-주석block-comment)
    * [한줄 주석](#한줄-주석-inline-comment)
  * [SQL 기초 설명](#sqlstructured-query-language-기본-설명)
  * [SELECT](#select-문법)
  * [WHERE](#where-문법)
  * [SELECT 문제 연습](#select-문제연습)
  * [WHERE 문제 연습](#where-문제연습)
  
  

 ## 블록 주석(block comment)
 /*

 (작성할내용)

 */

## 한줄 주석 inline comment
- -- (작성할 내용)

## SQL(Structured Query Language) 기본 설명
- SQL 문장은 세미콜론(;)으로 끝남.
- Ctrl+Enter:
- (1) 현재 커서가 있는 위치의 한 문장을 실행.
- (2) 드래그(drag)로 선택된 문장을 실행.
- F5: 스크립트(파일) 전체를 실행.

- bonus 테이블에서 모든 컬럼의 내용을 검색:
```sql
  - SELECT * FROM bonus;
```
- SQL 문장에서 명령어(키워드), 테이블 이름, 컬럼 이름은 대/소문자를 구분하지 않음.
- 테이블에 저장된 문자열 값들은 대/소문자를 구분함.

```sql
  - SELECT * FROM DEPT;

  - SELECT * FROM emp;

  - SELECT * FROM salgrade;
```
## SELECT 문법
- Alt+F10: SQL 새 워크시트 만들기.
```sql
- select 컬럼 이름, ... from 테이블 이름;
- select * from table; 테이블에서 모든 컬럼을 검색.
```
---
```sql
- emp: 직원 테이블, dept: 부서 테이블
- 직원 테이블에서 사번(empno), 직원 이름(ename)을 검색:
- select empno, ename from emp;
- select ename, empno from emp;
```
---
``
### 부서 테이블에서 모든 컬럼을 검색.
```sql
- select * from dept;
- select deptno, dname, loc from dept;
```
---
### 컬럼 이름에 별명(alias) 주기: as "별명"
```sql
- 별명을 줄 때는 반드시 큰따옴표("")만 사용함!
- 별명 이외의 문자열 값을 표현할 때는 작은따옴표('')를 사용!
- select deptno as "부서 번호", dname as "부서 이름"
from dept;
```
---
### 검색할 때 원하는 컬럼에만 별명을 줄 수 있음.
```sql
- select deptno as "부서 번호", dname
 from dept;
 ```
---
### 연결 연산자(||): 2개 이상의 컬럼을 합쳐서 하나의 컬럼으로 출력.
```sql
- '부서번호-부서이름' 형식의 문자열을 "부서 정보"라는 컬럼으로 출력:
- select deptno || '-' || dname as "부서 정보"
from dept;
```
---
### 부서 테이블을 검색해서 '... 부서는 ...에 있습니다.' 형식으로 결과 출력:
```sql
select
    dname || ' 부서는' || loc || '에 있습니다.' as "부서 정보"
from dept;
```
---
### 검색 결과를 정렬해서 출력하기:
```sql
- select 컬럼 이름, ... from 테이블 order by 컬럼 [asc/desc];
- asc: 오름차순(ascending order) 정렬. 기본값. asc는 생략 가능.
- desc: 내림차순(descending order) 정렬.
```

### 부서 테이블의 모든 컬럼을 검색, 부서 번호 내림차순으로 출력:
```sql
select * from dept order by deptno desc;
```
### 부서 테이블의 모든 컬럼을 검색, 부서 이름 오름차순으로 출력:
```sql
select * from dept order by dname;
```
### 직원 테이블에서 사번, 이름, 급여를 검색, 사번 오름차순으로 출력:
```sql
select empno, ename, sal from emp order by empno;
```
### 직원 테이블에서 사번, 이름, 급여를 검색, 급여 내림차순으로 출력:
```sql
select empno, ename, sal from emp order by sal desc;
```
####  SELECT 문제연습
```sql
-- 직원 테이블에서 부서번호, 사번, 이름을 검색
-- 정렬 순서: (1) 부서번호 오름차순, (2) 사번 오름차순
select deptno, empno, ename
from emp
order by deptno, empno;
```
```sql
-- 직원 테이블에서 부서번호, 이름, 급여를 검색
-- 정렬 순서: (1) 부서번호 오름차순, (2) 급여 내림차순
select deptno, ename, sal
from emp
order by deptno, sal desc;
```
```sql
-- 중복되지 않는 결과만 출력하기:
select job from emp;
select distinct job from emp; -- 중복되지 않는 업무이름들을 검색
-- (중복되지 않는) 업무 이름을 오름차순 정렬 출력:
select distinct job from emp order by job;

-- 중복되지 않는 부서번호, 직무를 출력, 부서번호 오름차순 정렬:
select distinct deptno, job from emp
order by deptno;
```
## WHERE 문법


## 테이블에서 데이터 검색:
```sql
  (1) projection: 테이블에서 원하는 컬럼들을 선택.
  (2) selection: 테이블에서 조건을 만족하는 행(레코드)들를 검색.
문법: select 컬럼, ... from 테이블 where 조건식 order by 컬럼, ...;
조건식에서 사용되는 연산자들:
  (1) 비교 연산자: =, !=, >, >=, <, <=, is null, is not null, ...
  (2) 논리 연산자: and, or, not
```
### WHERE 문제연습
```sql
-- 직원 테이블에서 10번 부서에서 근무하는 직원들의 부서번호, 사번, 이름 출력.
-- 정렬 순서: 사번
select deptno, empno, ename
from emp
where deptno = 10
order by empno;
```
```sql
-- 직원 테이블에서 수당(comm)이 null이 아닌 직원들의 
-- 사번, 부서번호, 이름, 수당을 출력.
-- 정렬 순서: 사번
select empno, deptno, ename, comm
from emp
where comm is not null
order by empno;
```
```sql
-- 직원 테이블에서 급여가 2000 이상인 직원들의 이름, 직무, 급여를 출력.
select ename, job, sal
from emp
where sal >= 2000;
```
```sql
-- 직원 테이블에서 급여가 2000 이상 3000 이하인 직원들의
-- 이름, 직무, 급여를 출력.
-- 정렬 순서: 급여.
select ename, job, sal
from emp
where sal >= 2000 and sal <= 3000
order by sal;
-- 또는 다른 문법으로 ↓
-- between = BETWEEN 연산자는 주어진 범위의 값을 선택합니다. 값은 숫자, 텍스트 또는 날짜일 수 있습니다. BETWEEN 연산자는 시작 및 끝 값을 포함하는 데이터를 선택합니다.
select ename, job, sal
from emp
where sal between 2000 and 3000
order by sal;
```
```sql
-- 직원 테이블에서 10번 부서 또는 20번 부서에서 근무하는
-- 직원들의 부서번호, 이름, 급여를 검색.
-- 정렬 순서: (1) 부서 번호 오름차순, (2) 급여 내림차순.
select deptno, ename, sal
from emp
where deptno = 10 or deptno = 20
order by deptno, sal desc;
-- 또는 다른 문법으로 ↓
-- in = - 조건절에서 사용하며 다수의 비교값과 비교하여 비교값 중 하나라도 같은 값이 있다면 true 이다.
select deptno, ename, sal 
from emp
where deptno in (10, 20) 
order by deptno, sal desc;
```
```sql
-- 직원 테이블에서 직무가 'CLERK'인 
-- 직원들의 직무, 이름, 급여를 출력.
-- 정렬 순서: 이름.
SELECT job, ename, sal
from emp
where job = 'CLERK'
order by ename;
```
```sql
-- 직원 테이블에서 직무가 'CLERK' 또는 'MANAGER'인 
-- 직원들의 직무, 이름, 급여를 검색.
-- 정렬 순서: (1) 직무, (2) 급여.
SELECT job, ename, sal
from emp
where job in('CLERK','MANAGER')
order by job,sal; 
```
```sql
-- 직원 테이블에서 20번 부서에서 근무하는 CLERK의 
-- 모든 정보(컬럼)을 검색.
SELECT *
FROM emp
WHERE deptno = 20;
```

```sql
-- 직원 테이블에서 CLERK, ANALYST, MANAGER가 아닌 
-- 직원들의 사번, 이름, 직무, 급여를 검색
-- 정렬 순서: 사번.
SELECT empno, ename, job, sal
FROM emp
WHERE job not in('CLERK','ANALYST','MANAGER')
ORDER BY empno;
```