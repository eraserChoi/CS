### 1\. DML(Data Manipulation Language)

   1) INSERT

     - 단일 행 INSERT 문은 VALUES 절을 포함하며, 한 번에 한 행만 입력된다

> INSERT INTO 테이블명 \[(칼럼1, 칼럼2, ...)\] VALUES (값1, 값2, ...);

    - INSERT문에 서브 쿼리를 사용하면 서브 쿼리의 결과를 테이블에 입력 가능.

      (단 INTO 절의 칼럼명 개수와 서브 쿼리의 SELECT 절 칼럼 개수가 일치해야한다.)

> INSERT INTO 테이블명 \[(칼럼1, 칼럼2, ..)\]  
> 서브 쿼리;

  2) UPDATE

      - 입력한 데이터 중 변경이 발생해 데이터를 수정해야 하는 경우 사용한다.

      - WHERE 절에서 수정 대상이 될 행을 식별할 수 있도록 조건식을 기술한다.

      - 만약 WHERE절을 사용하지 않는다면 테이블의 전체 데이터가 수정된다.

> UPDATE 테이블명  
>   SET 수정할 칼럼명 1= 수정될 새로운 값1  
>   .....  
> WHERE 조건

 3) DELETE

     - 테이블에 들어있는 데이터를 삭제할 때 사용한다.

     - 기본적으로 DELETE FROM 다음에 삭제를 원하는 자료가 저장된 테이블 명을 입력하고 실행한다.

     - WHERE절을 사용하지 않는다면 테이블의 전체 데이터가 삭제된다.

> DELETE FROM 테이블명  
> \[WHERE 삭제 대상 식별 조건식\];

 4) MERGE

   - 새로운 행을 입력하거나, 기존 행을 수정하는 작업을 한 번에 할 수 있다.

> MERGE  
>  INTO 타겟 테이블명  
> USING 소스 테이블명  
>    ON (조인 조건식)  
> WHEN MATCHED THEN  
>    UPDATE  
>      SET 수정할 칼럼명1 = 수정될 새로운 값1  
> WHEN NOT MATCHED THEN  
>     INSERT \[(칼럼1, 칼럼2, ...)\]  
>     VALUES (값1, 값2,...)
>     

### 1\. 트랜잭션 개요

    - 데이터베이스의 논리적 연산단위다.

    - 분할할 수 없는 최소의 단위이다.

[##_Image|kage@Aoh4T/btq0SHr0Jzi/JNuLozHZfvihwIH7pucgY1/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|||_##]

###   2. COMMIT

     - 입력, 수정, 삭제한 데이터에 대해 전혀 문제가 없다고 판단됐을 경우 COMMIT 명령어로 트랜잭션을 완료할 수 있다.

    - COMMIT이나 ROLLBACK 이전의 데이터 상태는 다음과 같다.

         - 데이터의 변경을 취소해 이전 상태로 복구 가능

         - 현재 사용자는 SELECT 문장으로 결과 확인 가능

         - 다른 사용자는 현재 사용자가 수행한 명령의 결과를 볼 수 없음

         - 변경된 행은 잠금이 설정돼서 다른 사용자가 변경할 수 없다.

  - COMMIT 이후의 데이터 상태는 다음과 같다.

        - 데이터에 대한 변경 사항이 데이터베이스에 반영된다.

        - 관련된 행에 댛나 잠금이 풀리고, 다른 사용자들이 조작 가능하다.

  - COMMIT 종류

     1) AUTO COMMIT

        - 기본 방식이며 DML과 DDL을 수행할 때 마다 DBMS가 트랜잭션을 컨트롤하는 방식이다.

        - 명령어가 성공적으로 수행되면 자동으로 COMMIT 수행

        - 오류가 발생하면 자동으로 ROLLBACK 수행

   2) 암시적 트랜잭션

       - 트랜잭션의 시작은 DBMS가 처리

       - 끝은 사용자가 명시적으로 COMMIT, ROLLBACK으로 처리한다.

  3) 명시적 트랜잭션

      - 트랜잭션의 시작과 끝을 사용자가 지정하는 방식이다.

      - BEGIN TRANSACTION(BEGIN TRAN)으로 시작하고, 2)와 같이 COMMIT, ROLLBACK으로 끝낸다.

### 3\. ROLLBACK

  - COMMIT 이전까지의 변경 사항에 대해 쥐소할 수 있다.

### 4\. SAVEPOINT

  - svaepoint를 정의하면 ROLLBACK할 때 틀정 부분까지 롤백이 가능하다.

> SAVEPOINT SVPT1;  
>   
> ROLLBACK TO SVPT1
