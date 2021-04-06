### 1\. 예상 실행계획

  사용자가 요청한 SQL을 최적으로 수행하고자 DBMS 내부적으로 수립한 일련의 처리 절차다.

ORACLE

####  가. Explain plan 

    - SQL문을 분석하고 해석하여 실행계획 수립 후 PLAN\_TABLE에 저장하도록 해주는 명령어

> EXPLAIN PLAN set statement\_id = 'query1' <--- set statement\_id = 는 생략 가능하다.  
> for select \* from emp where empno = 1;

####  나. AutoTrace

   - 실행계획뿐만 아니라 여러가지 유용한 실행통계를 확인할 수 있다.

>  SET AUTOTRACE on  
> select sum(1) from code;

[##_Image|kage@EC8Do/btq1WJ3XNsm/gdFlGNfbBRTqnzA9LRG8C0/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|출처 :&nbsp;http://www.gurubee.net/lecture/4152||_##]

     AUTOTRACE뒤에 옵션을 줄 수 있는데 다음과 같다

        1) on, on explain, on statistics -> 이는 실제 수행결과를 출력해야 하므로 쿼리를 실제 수행한다.

        2) traceonle, traceonly statistics -> 실행통계를 보여줘야 하므로 쿼리를 실제 수행한다.

        3) traceonly explain -> 실행계획만 출력하면 되므로 쿼리를 실제 수행하지 않는다.

####   다. DBMS\_XPLAN패키지

     - Oracle 9.2부터 plan\_table에 저장된 실행계획을 좀 더 쉽게 출력해 볼 수 있게 됐다.

    1) 예상 실행계획 출력

       -  첫번째 인자에는 실행 계획이 저장된 plan\_table명을 입력하고, 두번째 인자가 순서(NULL일 경우 가장 마지막)의

         explain\_plan을 보여주며, 세번째 인자를 통해 5(Basic, Typical, All, Outline, Advance)가지 포맷 옵션을 선택함.

> select plan\_table\_output from table (dbms\_xplan.display('plan\_table',null,'all'));

[##_Image|kage@dmmhTc/btq1WJQqEGJ/vsshKm7iQRnfQ4fVEKfXI1/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|질의문||_##][##_Image|kage@uImVJ/btq1YkCouwp/s5kuYRHbdUwWjxKkp2WZmk/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="860" height="NaN" data-ke-mobilestyle="widthContent"|출처 :&nbsp;http://wiki.gurubee.net/pages/viewpage.action?pageId=23429144||_##]

    2) 캐싱된 커서의 실제 실행계획 출력 

      - 커서란 하드파싱 과정을 거쳐 메모리에 적재된 SQL과 Parse Tree, 실행계획 등 실행하는데 필요 정보를 담은 Area

      - 오라클은 라이브러리 캐시에 캐싱되어 있는 수행 통계를 볼 수 있도록 v$sql 뷰를 제공

      - dbms\_xplan.display\_cursor함수를 통해 조회 가능

> SQL> select \* from table (dbms\_xplan.display\_cursor('sql\_id',child\_no,'format'));

[##_Image|kage@ojNpQ/btq1XK2n2SX/5pGk0aaM5ZhEmQxLEuxqyk/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|||_##]

## 2\. SQL 트레이스

   - 실제로 수행된 정보가 저장되어 있다.

   - Autotrace만으로 부하의 원인을 찾기 어려울 때 내부 수행 절차상 어느 단계에서 부하를 일으키는 지 확인 가능

[##_Image|kage@9Qhn2/btq1V1RAmw8/o6kjIgHJ4Fu91AJbvTHVk0/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|출처 :&nbsp;http://wiki.gurubee.net/pages/viewpage.action?pageId=23429127||_##]

   - Elapsed Time은 Call단위로 측정이 이루어짐 (CPU time + Wait Time = Response시정 - Call시점)

   - Call 발생 횟수

       Select문 = Parse Call + Execute Call + Fetch Call

       DML문   = Parse Call + Execute Call

## 3\. 응답 시간 분석

    - 프로세스 간에는 상호작용하면서 다른 프로세스가 일을 마칠 때까지 기다려야 한다.

    - 일을 진행할 수 있을 떄까지 수면(Sleep) 상태로 대기한다.

    - 그 기간 정해진 간격으로 각 대기 유형별 상태와 시간 정보가 공유 메모리 영역에 저장된다.(최대치만 저장됨)

   가. 라이브러리 캐시 부하 - 라이브러리 캐시에서 SQL커서를 찾고 최적화하는 과정에서 경합 발생  
   나. 데이터베이스 Call과 네트워크 부하 - 애플리케이션과 네트워크 구간에서 소모된 시간

   다. 디스크 I/O부하 - 디스크(Block)을 읽는데 사용된 시간

   라. 버퍼 캐시 경합 - 버퍼 캐시를 읽는데 소요되는 시간

   마. Lock 관련 대기 이벤트
