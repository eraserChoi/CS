# 데이터베이스
&nbsp;&nbsp; 흔히 현대 사회를 가리켜 정보화 사회라고 한다. 그만큼 일상생활에서 다양한 정보가 나오고, 이러한 점보를 수집, 처리하고 분석, 으용하는 것은 현대 사회 어느 곳에서나 필요한 요소가 됐다.</br>
&nbsp;&nbsp; 넓은 의미에서 데이터베이스는 이러한 일상적인 정보를 모아 놓은 것 자체를 의미한다. 그러나 특정 기업이나 조직, 개인이 필요에 따라 데이터를 일정한 형태로 저장해 놓은 것을 의미한다.</br>
&nbsp;&nbsp; DBMS(Database Management System)는 더 효율적인 데이터 관리뿐 아니라 예기치 못한 사건으로 인한 데이터 손상을 피하고, 필요한 데이터를 복구하기 위한 강력한 기능을 제공하는 시스템을 의미한다.</br>
</br>

# SQL(Structured Query Language)
&nbsp;&nbsp; 관계형 데이터베이스에서 데이터 정의, 데이터 조작, 데이터를 제어하기 위해 사용하는 언어이다. </br>
&nbsp;&nbsp; SQL의 최초 이름이 SEQUEL이었기 때문에 시큐얼로 읽는 사람도 있지만, 표준은 '에스큐엘'로 읽는다.</br>
&nbsp;&nbsp; 다른 언어보다 기초 단계 학습은 쉽지만, 고급 SQL(SQL튜닝 등...)로 들어갈 수록 어려워 진다. </br>
</br>
</br>

# 데이터 조작어(DML, Data Manipulation Language)
  > 저장한 데이터를 처리하는데 사용하는 언어

명령어      |       기 능
---------- | ---------------------------------------------------
SELECT      | 테이블에서 조건에 맞는 튜플을 검색함
INSERT      | 테이블에 새로운 튜플을 삽입함
DELETE      | 테이블에서 조건에 맞는 튜플을 삭제함
UPDATE      | 테이블의 조건에 맞는 튜플의 내용을 변경함

</br>
</br>

# 데이터 정의어(DDL, Data Definition Language)
  > SCHEMA, DOMAIN, TABLE, VIEW, INDEX를 정의하거나 변경 또는 삭제할 때 사용하는 언어

명령어      |       기 능
---------- | ---------------------------------------------------
CREATE      | 스키마, 도메인, 테이블, 뷰, 인덱스를 정의함
ALTER      | 테이블에 대한 정의를 변경하는데 사용함
DROP      | 스키마, 도메인, 테이블, 뷰, 인덱스를 삭제함
RENAME      | 스키마, 도메인, 테이블, 뷰, 인덱스의 이름을 변경함
</br>
</br>

# 데이터 제어어(DCL, Data Control Language)
  > 데이터베이스에 접근하고 객체들을 사용하도록 권한을 주고 회수하는 명령어

  명령어      |       기 능
---------- | ---------------------------------------------------
GRANT      | 데이터베이스 사용자의 사용 권한을 부여함
REVOKE      | 데이터베이스의 사용자의 사용 권한을 취소함

</br>
</br>

# 트랜잭션 제이어(TCL, Transaction Control Language)
  > 결과를 작업단위(트랜잭션)별로 제어하는 명령어

명령어      |       기 능
---------- | ---------------------------------------------------
COMMIT     | 데이터베이스 조작 작업이 정상적으로 완료되었음을 관리자에게 알려줌
ROLLBACK      | 데이터베이스 조작 작업이 비정상적으로 종료되었을 때 원래의 상태로 복구함.

</br>
</br>


# STANDARD SQL 개요

IBM DB2나 SYBASE ASE DBMS와 Oracle 같이 다른 시스템간의 DBMS의 SQL명령어는 달랐으나, ANSI/ISO SQL에 의해 DBMS간 평준화를 이루어 가고 있다.
</br>
</br>


# 일반 집합 연산자 

연산자      |       기 능
---------- | ---------------------------------------------------
Union      | 수학의 합집합으로 중복된 값을 없애서 보여준다. 그러나 중복된 값을 없애기 위해 부하가 생긴다. 추후에 중복된 값도 출력하는 UNION ALL이 나왔다.
Intersction      | 수학의 교집합으로 두 집합의 공통집합을 추출한다.
Difference     | 수학의 차집합으로 첫 번째 집합에서 두 번째 집합과의 공통집합을 제와한 부분이다.<br>SQL표준에는 EXCEPT로 표시되어 있으나 Oracle은 MINUS로 되어있다.
Product      | 수학의 곱집합으로, JOIN조건이 없는 경우 생길 수 있는 모든 데이터의 조합을 말한다.<br>양쪽 집합의 M*N건의 데이터 조합이 발생하며 CARTESIAN(데카르트) PRODUCT라고 표현한다.

</br>
</br>

# 순수 관계 연산자
  > 관계형 데이터베이스를 구현하기 위해 새롭게 만들어진 연산자.

연산자      |       기 능
---------- | ---------------------------------------------------
SELECT      | 특정 열을 보여준다. *로 하면 모든 열이 표시된다.
PROJECT      | 특정 행을 보여준다.
NATURAL JOIN     | 두 테이블 간의 동일한 이름을 갖는 모든 칼럼에 대해 연결한다.
DIVIDE      | 특정 값이 없는 값을 출력한다. 현재 사용되지 않는 연산이다.

# FROM 절 JOIN 형태
  > ANSI/ISO SQL에 표시하는 FROM절의 JOIN형태는 다음과 같다.

* INNER JOIN
* NATURAL JOIN
* USING 조건절
* ON 조건절
* CROSS JOIN
* OUTER JOIN

</br>
</br>

# 테이블 정보

<p align="center">
    <img style="width:200px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0216/emp.jpg?raw=true"> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <img style="width:200px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0216/dept.jpg?raw=true"><br/>
    EMP Table&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    DEPT Table
</p>

# INNER JOIN
* INNTER JOIN은 JOIN 조건에서 동일한 값이 있는 행만 반환한다.
* USING 조건절이나 ON 조건절을 필수적으로 사용해야 한다.



```
SELECT A.DEPTNO, A.EMPNO, A.ENAME, B.DNAME
FROM   EMP A, DEPT B
WHERE  A.DEPTNO = B.DEPTNO ;
```
위와 아래는 같은 결과를 반환하다.
```
SELECT A.DEPTNO, A.EMPNO, A.ENAME, B.DNAME
FROM   EMP A INNER JOIN DEPT B
WHERE  A.DEPTNO = B.DEPTNO ;
```
INNER를 생략할 수 있다. 
```
SELECT A.DEPTNO, A.EMPNO, A.ENAME, B.DNAME
FROM   EMP A  JOIN DEPT B
WHERE  A.DEPTNO = B.DEPTNO ;
```
<p align="center">
  <img style="width:400px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0216/innerjoin.jpg?raw=true"><br/>
  INNERJOIN 결과 값
</p>

</br>
</br>

# NATURAL JOIN
  * 두 테이블 간의 동일한 이름을 갖는 모든 칼럼들에 대해 EQUI(=) JOIN을 수행한다.

```
SELECT DEPTNO, EMPNO, ENAME, DNAME
FROM   EMP NATURAL JOIN DEPT ;
```

<p align="center">
  <img style="width:400px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0216/naturaljoin.jpg?raw=true"><br/>
  NATURAL JOIN 결과 값
</p>

</br>
</br>

# USING 조건절
* NATURAL JOIN에서는 모든 일치되는 칼럼들에 대해 JOIN이 이루어지지만, FROM 절의 USING 조건절을 이용하면 같은 이름을 가진 칼럼들 중에서 원하는 칼럼에 대해서만 선택적으로 EQUI JOIN을 할 수가 있다

```
SELECT *
FROM DEPT JOIN EMP
USING (DEPTNO);
```
<p align="center">
  <img style="width:400px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0216/using%EC%A0%88.jpg?raw=true"><br/>
  USING 조건절 결과 값
</p>

</br>
</br>

# ON 조건절
* 칼럼명이 다르더라도 JOIN 조건을 사용할 수 있는 장점이 있다.

```
SELECT E.EMPNO, E.ENAME, E.DEPTNO, D.DNAME
FROM   EMP E JOIN DEPT D
ON     (E.EMPNO = D.DEPTNO);
```

<p align="center">
  <img style="width:400px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0216/on%EC%A0%88.jpg?raw=true"><br/>
  ON 조건절 결과 값
</p>

</br>
</br>


# CROSS JOIN
* 두 개의 테이블에 대한 M*N건의 데이터 조합이 발생한다.

```
SELECT ENAME,  DNAME
FROM   EMP CROSS JOIN DEPT
ORDER  BY ENAME;
```

<p align="center">
  <img style="width:400px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0216/crossjoin.jpg?raw=true"><br/>
  CROSS JOIN 조건절 결과 값
</p>

</br>
</br>


# OUTER JOIN
* JOIN 조건에서 동일한 값이 없는 행도 반환할 때 사용할 수 있다.

```
SELECT *
FROM   EMP E LEFT OUTER JOIN DEPT D
ON     E.DEPTNO = D.DEPTNO;
```

<p align="center">
  <img style="width:400px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0216/outerjoin.jpg?raw=true"><br/>
  OUTER JOIN 조건절 결과 값
</p>

</br>
</br>



