---
title: sql
date: 2021-11-02 13:07:29
tags: sql
---

--테이블 삭제
DROP TABLE EMPLOYEE;
DROP TABLE DEPARTMENT;
DROP TABLE SALGRADE;
--테이블 생성
CREATE TABLE DEPARTMENT
        (DNO NUMBER(2) CONSTRAINT PK_DEPT PRIMARY KEY,
         DNAME VARCHAR2(14),
	 LOC   VARCHAR2(13) ) ;
CREATE TABLE EMPLOYEE 
        (ENO NUMBER(4) CONSTRAINT PK_EMP PRIMARY KEY,
	 ENAME VARCHAR2(10),
 	 JOB   VARCHAR2(9),
	 MANAGER  NUMBER(4),
	 HIREDATE DATE,
	 SALARY NUMBER(7,2),
	 COMMISSION NUMBER(7,2),
	 DNO NUMBER(2) CONSTRAINT FK_DNO REFERENCES DEPARTMENT);
CREATE TABLE SALGRADE
        (GRADE NUMBER,
	 LOSAL NUMBER,
	 HISAL NUMBER );
--테이블 데이터 입력
INSERT INTO DEPARTMENT VALUES (10,'ACCOUNTING','NEW YORK');
INSERT INTO DEPARTMENT VALUES (20,'RESEARCH','DALLAS');
INSERT INTO DEPARTMENT VALUES (30,'SALES','CHICAGO');
INSERT INTO DEPARTMENT VALUES (40,'OPERATIONS','BOSTON');

INSERT INTO EMPLOYEE VALUES
(7369,'SMITH','CLERK',    7902,to_date('17-12-1980','dd-mm-yyyy'),800,NULL,20);
INSERT INTO EMPLOYEE VALUES
(7499,'ALLEN','SALESMAN', 7698,to_date('20-2-1981', 'dd-mm-yyyy'),1600,300,30);
INSERT INTO EMPLOYEE VALUES
(7521,'WARD','SALESMAN',  7698,to_date('22-2-1981', 'dd-mm-yyyy'),1250,500,30);
INSERT INTO EMPLOYEE VALUES
(7566,'JONES','MANAGER',  7839,to_date('2-4-1981',  'dd-mm-yyyy'),2975,NULL,20);
INSERT INTO EMPLOYEE VALUES
(7654,'MARTIN','SALESMAN',7698,to_date('28-9-1981', 'dd-mm-yyyy'),1250,1400,30);
INSERT INTO EMPLOYEE VALUES
(7698,'BLAKE','MANAGER',  7839,to_date('1-5-1981',  'dd-mm-yyyy'),2850,NULL,30);
INSERT INTO EMPLOYEE VALUES
(7782,'CLARK','MANAGER',  7839,to_date('9-6-1981',  'dd-mm-yyyy'),2450,NULL,10);
INSERT INTO EMPLOYEE VALUES
(7788,'SCOTT','ANALYST',  7566,to_date('13-07-1987', 'dd-mm-yyyy'),3000,NULL,20);
INSERT INTO EMPLOYEE VALUES
(7839,'KING','PRESIDENT', NULL,to_date('17-11-1981','dd-mm-yyyy'),5000,NULL,10);
INSERT INTO EMPLOYEE VALUES
(7844,'TURNER','SALESMAN',7698,to_date('8-9-1981',  'dd-mm-yyyy'),1500,0,30);
INSERT INTO EMPLOYEE VALUES
(7876,'ADAMS','CLERK',    7788,to_date('13-07-1987', 'dd-mm-yyyy'),1100,NULL,20);
INSERT INTO EMPLOYEE VALUES
(7900,'JAMES','CLERK',    7698,to_date('3-12-1981', 'dd-mm-yyyy'),950,NULL,30);
INSERT INTO EMPLOYEE VALUES
(7902,'FORD','ANALYST',   7566,to_date('3-12-1981', 'dd-mm-yyyy'),3000,NULL,20);
INSERT INTO EMPLOYEE VALUES
(7934,'MILLER','CLERK',   7782,to_date('23-1-1982', 'dd-mm-yyyy'),1300,NULL,10);

INSERT INTO SALGRADE VALUES (1, 700,1200);
INSERT INTO SALGRADE VALUES (2,1201,1400);
INSERT INTO SALGRADE VALUES (3,1401,2000);
INSERT INTO SALGRADE VALUES (4,2001,3000);
INSERT INTO SALGRADE VALUES (5,3001,9999);
--커밋
COMMIT;
--확인하기
select*from tab;

select*from employees;
select*from department;
select*from salgrade;
--내림차순정리
desc employee;
select *from tab;
select sysdate from dual;
desc dual;

select eno,ename,salary,salary*12 from employee;

select eno,ename,salary+nvl(commission,0),salary*12 as 연봉 from employee;

select distinct dno from employee;
select dno from employee;

select*from employee where salary >= 1500;
select *from employee where job = 'ANALYST';

select eno,ename,salary from EMPLOYEE where ename=SCOTT;
select eno,ename,salary from employee where ename='SCOTT';
select eno,ename,salary from employee where ename>'SCOTT';
select*from employee where hiredate<='1981/01/01';

select*from employee where dno=10 and job ='MANAGER';
select*from employee where dno=10 or job = 'MANAGER';
select*from employee where not dno=10;

select*from employee where salary>=1000 and salary<=1500;
select*from employee where salary<1000 or salary>1500;
select*from employee where commission=300 or commission=500 or commission=1400;

select*from employee where not salary between 1000 and 1500;
select*from employee where hiredate between '1982/01/01' and '1983/01/01';

select*from employee where commission in(300,500,1400);
select*from employee where not commission in(300,500,1400);

select*from employee where ename like 'F%';
select*from employee where ename like '%M%';
select*from employee where ename like '%N';

select*from employee where ename like '_A%';
select*from employee where ename like '__A%';
select*from employee where not ename like '%A%';

select*from employee where commission is not null;

select*from employee order by ename; --desc asc

select*from employee order by salary asc;
select*from employee order by salary desc;

select*from employee order by salary desc,ename asc;

--1.select ename,salary,salary+300 from employee;

--2.select ename,salary,salary*12+100 from employee order by salary*12+100 desc;

--3.select ename,salary from employee where salary>2000 order by salary desc;

--4.select eno,ename,dno from employee where eno=7788;

--5.select ename,salary from employee where not salary>2000 and salary<3000;

--6.select ename,job,hiredate from employee where hiredate between '1981-02-20' and '1981-05-01';

--7.select dno,ename from employee where dno in(20,30) order by ename desc;

--8.select ename,dno,salary from employee where salary>=2000 and salary<=3000 and dno=20 or dno=30 order by ename;

--9.select ename,hiredate from employee where hiredate like '81%';

--10.select ename,job from employee where manager is null;

--11.select ename,salary,commission from employee where not commission=0 order by salary,commission desc;

--12.select*from employee where ename like '__R%';

--13.select*from employee where ename like '%A%' and ename like '%E';

--14.select ename,job,salary from employee where (job='CLERK' or job='SALESMAN') and not salary in(1600,950,1300);

--15.select ename,salary,commission from employee where commission>=500;

select to_char(sysdate,'yy/mm/dd/dy') from dual;

select ename, to_char(salary,'l999,999') from employee;

select ename,hiredate from employee where hiredate=to_date(810220);

select to_number('50,000','999,999') from dual;

select to_char(salary,'9999,99')from employee;

--0은 없는수는 0으로 효기 9는 아에 안뜸

--sum()합계 avg()평균 max()최대값 min()최소값 count()행의 개수 count(distinct)행의개수(중복1개만)
--stdev()표준편차 variance()분산

select sum(salary) as "급여총액" from employee;
--max
--min
--avg

select max(hiredate),min(hiredate) from employee;
select sum(commission) as "커미션 총액" from employee;

select count(commission) as "사원 수" from employee where commission is not null;

select count(distinct dno)from employee;

select job from employee order by job asc;
select count(job) as "직업 수 " from employee;
select count(distinct job) as "중복제외 직업수" from employee;

select avg(salary) as "급여평균" from employee group by dno;
select ename as "이름",dno as "부서번호" , avg(salary) from employee group by dno,ename;

select dno,job, sum(salary) from employee group by dno,job order by dno asc, job asc;
-- 정렬 순서 상관있음 앞에있는게 먼저 정렬

select job,sum(salary) as " 총액",round(avg(salary),1) as "평균액" from employee having avg(salary)>=2000 group by job;
--1.부서별 최고 급여 3000 이상 부서 번호 와 부서별 최고 급여
select job as "부서",dno as "부서번호",max(salary) as "최고급여" from employee having max(salary)>=3000 group by job,dno;
--2.매니저 제외 급여총액 5000이상 담당업무별 급여 총액과 해당인원
select job as "담당업무",count(job) as "해당 인원",sum(salary) as "급여 총액" from employee where job not like 'MANAGER' group by job having sum(salary)>=5000;
--3.부서별 평균 급여중 최고 평균 급여 조회
select max(avg(salary))as "최고평균급여" from employee group by dno;

--ROLLUP() 중간 합계
select job,sum(salary) from employee group by rollup(job);

--1번문제
select max(salary),min(salary),sum(salary),round(avg(salary)) from employee;
--2번문제
select job,max(salary),min(salary),sum(salary),round(avg(salary)) from employee group by job;
--3번문제
select job,count(job) from employee group by job;
--4번문제
select count(*) from employee where job like '%MANAGER%';
select count(distinct(manager)) from employee;--문제이상해
--5번문제
select max(salary)-min(salary)as "difference" from employee;
--6번문제
select job,min(salary) from employee where MANAGER is not null group by job having not min(salary)<2000 order by min(salary) desc;
--7번문제
select dno,count(job),round(avg(salary),2) from employee group by dno;

--내장함수
select ascii('t') from dual;
select chr(116) from dual;
select asciistr('천') from dual;
select unistr('\CC9C') from dual;

select length('한글'), lengthb('한글'), lengthc('한글')from dual;
--문자열 함수

select concat('이것은','오라클이다'),'이것이'||'오라클'||'이다' from dual;
select instr('이것이 oracle이다. 이것도 오라클이다.','이것')from dual;
select instr('이것이 oracle이다. 이것도 오라클이다.','이것',16)from dual; --문자열
select instrb('이것이 oracle이다. 이것도 오라클이다.','이것',2)from dual; --바이트단위

select lower('abcdefgh'),upper('abcdefgh'),initcap('thIs is oraCLe') from dual;
--lower 소문자 upper대문자 initcap 앞부분 대문자치환
select replace('이것이 oracle이다','이것이','this is') from dual;
select translate('이것이 oracle이다','이것','ab') from dual;

select ename, lower(ename), job,initcap(job) from employee;

--대소문자유의
select eno,ename,dno from employee where ename='scott';
select eno,ename,dno from employee where ename=upper('scott');
select eno,ename,dno from employee where initcap(ename)='Scott';

select substr('대한독립만세',2,5) from dual; --2가 글자열 5가 길이
select reverse('oracle') from dual;
select lpad('이것이',10,'웅') from dual; --lpad rpad
select ltrim('          이번생은'),rtrim('응앵ㅋㅋㅋㅋ','ㅋ')from dual; --ltrim rtrim
select trim('      이번생은       '), trim(both 'ㅋ' from 'ㅋㅋㅋ망했어욬ㅋㅋㅋ') from dual;
select regexp_count('이것이 오라클이다.','이') from dual;

select*from employee where substr(ename,-1,1)='N';

select*from employee where substr(hiredate,1,2)='87';

select lpad(salary,10,'#') from employee;

select rpad(salary,10,'#') from employee;

select add_months('2020-01-01',5), add_months(sysdate,-5) from dual;

select to_date('2020-01-01')+5,sysdate-5 from dual;

select current_date,sysdate,current_timestamp from dual;

select extract(year from date '2019-06-27'), extract(day from sysdate) from dual;

select last_day('2019-05-05') from dual;

select next_day('2020-01-03','월요일'), next_day(sysdate,'일요일') from dual;

select months_between(sysdate,'1985-02-17') from dual;

select hiredate,trunc(hiredate,'month') from employee;

select round(sysdate-hiredate) as 근무일수 from employee;

select sysdate, next_day(sysdate,'토요일') from dual;

select ename,hiredate,add_months(hiredate,6) from employee;

select ename, sysdate,hiredate, trunc(months_between(sysdate, hiredate)) from employee;

select ename,hiredate,last_day(hiredate) from employee;

select ename,salary, commission, nvl(commission,0), salary*12+nvl(commission,0) from employee;

select ename, salary,commission, nvl2(commission,salary*12+commission,salary*12) from employee;

select nullif('a','a'), nullif('a','b') from dual;

select ename,salary,commission, coalesce(commission,salary,0) from employee;

select ename,dno,decode(dno,10, 'accounting', 20,'research',30,'sales',40,'operations','default') as dename from employee;

select ename,dno, case when dno=10 then 'accounting' when dno=20 then 'research' when dno=30 then 'sales' when dno=40 then 'operations' else 'default' end as dename from employee;

--1번문제
select substr(hiredate,1,5) from employee;
--2번문제
select*from employee where substr(hiredate,5,1)='4';
--3번문제
--1번문제

create table productsTbl(productid char(20),
productName nvarCHAR2(20) not null,
price Number(*) not null,
amount Number(*) not null);

create table customerTbl(customerid char(10),
customername nvarchar2(20) not null,
customerAddr nvarchar2(100) not null,
customerContact char(11)not null);

create table tradeTbl(tradeno char(10),
productid char(10)not null,
customerid char(10)not null,
tradeAmount number(*)not null);

alter table productstbl add constraint pk_productsTbl_productid primary key(productid);
alter table customerTbl add constraint pk_customertbl_customerid primary key(customerid);
alter table tradeTbl add constraint pk_tradeTbl_tradeNo primary key(tradeNo);

alter table tradetbl 
add constraint tradetbl_productstbl_FK foreign key(productid) references productstbl(productid);
alter table tradetbl
add constraint tradetbl_customertbl_KR foreign key(customerid) references customertbl(customerid);
 
insert into productstbl
values('b001','JAVA','20000','100');
insert into productstbl
values('b002','HTMLCSS','15000','150');
insert into productstbl
values('b003','Python','17500','200');
insert into productstbl
values('b004','javaScript','17000','150');
insert into productstbl
values('b005','Oracle','25000','75');

insert into customertbl
values('S001','수주IT그룹','경기도 수원시',01012345678);
insert into customertbl
values('N001','남양 소프트웨어','경기도 화성시',01014753695);
insert into customertbl
values('K001','과주 IDC센터','경기도 과천시',01014753695);
insert into customertbl
values('K002','금주정보통신','경기도 시흥시',01098753215);
insert into customertbl
values('S002','서원 소프트','경기도 용인시',01012357895);

insert into tradetbl
values('t001','b003','S002',30);
insert into tradetbl
values('t002','b003','N001',40);
insert into tradetbl
values('t003','b004','S002',20);
insert into tradetbl
values('t004','b005','N001',40);
insert into tradetbl
values('t005','b004','K002',50);

commit;

select*from productstbl;
select*from customertbl;
select*from tradetbl;