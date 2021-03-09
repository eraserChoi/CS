### 1\. 서브 쿼리

   \* 하나의 SQL문안에 포함돼 있는 또 다른 SQL문을 말한다.

        1) 서브 쿼리는 괄호(.) 로 감싸서 기술한다.

        2) 단일 행, 복수행 비교 연산자와 함께 사용 가능하다.

        3) 중첩 서브 쿼리 및 스칼라 서브 쿼리에서는 ORDER BY 사용 불가.

            - SELECT문에 있는 서브 쿼리 : 스칼라 서브쿼리

            - FROM절에 있는 서브쿼리 : 인라인 뷰

            - WHERE절에 있는 서브쿼리 : 서브쿼리

[##_Image|kage@k1QFm/btqZvN3sIi5/k3tuFm4MH4PHLqofO4W56k/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|출처 :&nbsp;http://wiki.gurubee.net/pages/viewpage.action?pageId=27427331||_##]

   \* 왜 서브 쿼리를 사용해야 하는가?

       - 두 개 이상의 테이블의 결과 중 한 쪽 테이블의 결과만 필요할 때 연산수를 줄일 수 있음.

            \* 조인은 집합간 곱(Product)의 관계이다.

            \* M개의 테이블과 N개의 테이블 조인 시 MN의 연산이 발생

            \* 서브 쿼리는 M의 연산 중 일부 M\`N연산이 필요.

### 2\. 단일 행 서브 쿼리

   \* 단일 행 비교 연산자(=, <, <=, >, >=, <> 등)와 함께 사용될 때 서브 쿼리의 결과 건수가 반드시

      1건 이하이어야 한다.

         - 2개 이상이면 Runtime오류 발생, 또는 맨 위의 행만 참조.

> SELECT \*  
> FROM \[OrderDetails\]  
> WHERE OrderID = (SELECT OrderID  
>                           FROM \[Orders\]  
>                           order by OrderID asc);

[##_Image|kage@rATNl/btqZFto1G9M/db2ckR9y6eJc2okuoA3SK1/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|오름차순 시 OrderID가 10248이 반환||_##]

> SELECT \*  
> FROM \[OrderDetails\]  
> WHERE OrderID = (SELECT OrderID  
>                           FROM \[Orders\]  
>                           order by OrderID desc);

[##_Image|kage@brsyJ8/btqZDPMPQ7a/35Ou69mGsKJLYwzFQlLzY0/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|내림차순 시 OrderID가 10443이 반환||_##]

### 3\. 다중 행 서브 쿼리

    - 서브 쿼리의 결과가 2건 이상 반환될 수 있다면, 다중 행 비교 연산자(IN, ALL, ANY, SOME0와 함께 사용해야 한다.

[##_Image|kage@MNURK/btqZECmdRwL/mPaQ0Pa4KUfBeXD3IKejA1/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|||_##][##_Image|kage@cki8uC/btqZvM4uvjm/OU0iaoJtcYINK81jKkVfn1/img.png|alignCenter|data-origin-width="0" data-origin-height="0" width="635" height="NaN" data-ke-mobilestyle="widthContent"|||_##]

### 4\. 다중 칼럼 서브 쿼리

    - 서브 쿼리의 결과로 여러 개의 칼럼이 반환돼 메인 쿼리의 조건과 동시에 비교되는 것을 의미

    - 다중 열 서브 쿼리와 같이 다중 행 비교 연산자를 이용해서 비교한다.

### 5\. 연관 서브 쿼리

    - 서브 쿼리 내에 메인 쿼리 칼럼이 사용된 서브 쿼리이다.

         \* 질의하고 싶은 테이블과 동일한 테이블을 서브 쿼리의 테이블로 사용하는 경우

         \* 만약 특정 테이블에 있는 평균 값 이상인 테이블만 출력하고 싶은 경우.

<table style="border-collapse: collapse; width: 100%; height: 73px;" border="1"><tbody><tr style="height: 73px;"><td style="width: 50%; text-align: center; height: 73px;">[##_Image|kage@bZaihJ/btqZEBnieMJ/kVSWTI5MkwojIJevlh7yY0/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|||_##]<p>틀린방법</p></td><td style="width: 50%; text-align: center; height: 73px;">[##_Image|kage@bPRDvj/btqZKzu0P1W/z1Em37mDUz8s3ArUJXzPwK/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|||_##]<p>옳은 방법</p></td></tr></tbody></table>

[##_Image|kage@cveE8V/btqZBdtKK2n/6SUIEzWjr4IwZ6uxjuzQzk/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|평균은 약 24.6이다.||_##]

### 6\. 뷰(View)

   \* 실제 데이터를 가지고 있지 않고, 단지 뷰 정의(View Definition)만ㅇ르 갖고 있다.

   \* 질의에서 뷰가 사용되면 뷰 정의를 참조해서 DBMS 내부적으로 질의를 재작성해 질의를 수행한다.

   \* 뷰를 가상 테이블(Virtual Table)이라고도 한다.

[##_Image|kage@ntbOC/btqZFtWVprv/t5dKly2OYUIPZ5zfHPBVG0/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|http://wiki.gurubee.net/pages/viewpage.action?pageId=27427331||_##]

  \* CREATE VIEW를 이용해서 생성하고 DROP VIEW을 이용해서 삭제 가능

<table style="border-collapse: collapse; width: 100%;" border="1"><tbody><tr><td style="width: 50%;">[##_Image|kage@GvZ2G/btqZDPsCdkP/gN0qAaSbH10SUCagouCeRK/img.png|alignCenter|data-origin-width="403" data-origin-height="90" data-ke-mobilestyle="widthContent"|||_##]</td><td style="width: 50%; text-align: center;">[##_Image|kage@mmbPw/btqZyv2uR8I/smYCmIwoN1kkf8v3xW8oQk/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|||_##]</td></tr></tbody></table>

### 7\. 그룹 함수

    \* 데이터 분석을 위해 소그룹 간의 소계를 계산하는 함수(ex) ROLLUP : 데이터의 총계

<table style="border-collapse: collapse; width: 100%;" border="1"><tbody><tr><td style="width: 50%; text-align: center;">[##_Image|kage@cY2Q4h/btqZIzI3TWP/44DHv1WAkGVUD5eiVJv6Yk/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|||_##]</td><td style="width: 50%; text-align: center;">[##_Image|kage@45XMF/btqZyvVNn3q/5eEgDlN4HkuzJfjUMKGPs0/img.png|alignCenter|data-origin-width="0" data-origin-height="0" data-ke-mobilestyle="widthContent"|||_##]</td></tr></tbody></table>

### 8\. 윈도우 함수

    \* 행과 행간의 관계를 쉽게 정의하기 위해 만든 함수(ex: RANK(순위))

### 9\. Top N 쿼리

    \* 상위(Top) N개의 행을 조회하는 쿼리다. Oracle은 ROWNUM, SQL Server은 TOP을 이용한다.
