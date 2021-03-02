# SELECT
&nbsp;&nbsp;* 사용자가 입력한 데이터는 언제라도 조회할 수 있다.</br>
&nbsp;&nbsp;* 입력된 데이터를 조회해보는 SQL 문이다.</br>

##  명령어</br>

### ALL / DISTINCT
&nbsp;&nbsp;* ALL : DEFAULT로 중복된 데이터를 출력한다.</br>
&nbsp;&nbsp;* DISTINCT : 중복된 데이터는 한개만 출력한다.(2개 컬럼 이상부터는 다 중복되어야 제거된다.)</br>
```
SELECT [ALL/DISTINCT] 출력 대상 칼럼명, 출력 대상 칼럼명, ...
   FROM 출력 대상 칼럼들이 있는 테이블명;
```
<p align="center">
    <img style="width:200px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0302/all.jpg?raw=true">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <img style="width:200px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0302/distinct.jpg?raw=true"><br/>
    ALL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    DISTINCT
</p>

### ALIAS 부여하기
&nbsp;&nbsp;* 조회한 결과에 일종의 별명(ALIAS, ALIASES)을 부여해 칼럼 레이블을 변경할 수 있다.</br>
&nbsp;&nbsp;&nbsp;&nbsp;- 칼럼명 바로 뒤에 온다.</br>
&nbsp;&nbsp;&nbsp;&nbsp;- 칼럼명과 ALIAS 사이에 AS, as 키워드를 사용할 수 있다.(옵션)</br>
&nbsp;&nbsp;&nbsp;&nbsp;- 이중 인용부호(Double quotation)는 ALIAS가 공백, 특수문자를 포함할 경우와 대소문자 구분이 필요할 때 사용한다.</br>
```
SELECT 출력 대상 칼럼명1  AS 이름, 출력 대상 칼럼명2 AS 성, 출력 대상 칼럼명3 As 생일, ...
    FROM 출력 대상 칼럼들이 있는 테이블명;
```

<p align="center">
    <img style="width:400px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0302/aliasNo.jpg?raw=true"><br/>
    기존 테이블 결과
</p>
<p align="center">
    <img style="width:400px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0302/aliasYes.jpg?raw=true"><br/>
    ALIAS 적용 결과
</p>

### 산술 연산자와 합성 연산자
&nbsp;&nbsp;* 산술 연산자 : NUMBER와 DATE자료형에 적용되며 , 4칙연산 결과와 동일하다.</br>
&nbsp;&nbsp;&nbsp;&nbsp;* 합성 연산자 : 문자와 문자를 연결하고 싶을 때 사용한다.</br>
</br>

#### 산술 연산자
```
SELECT 출력 대상 칼럼명1 + 대상 칼럼명2 AS 새로운 별칭, ...
    FROM 출력 대상 칼럼들이 있는 테이블명;
```
</br>

#### 합성 연산자
```
SELECT 출력 대상 칼럼명1 || '연결할 말(옵션)' || 대상 칼럼명2 AS 새로운 별칭, ...
    FROM 출력 대상 칼럼들이 있는 테이블명;
```
<p align="center">
    <img style="width:100px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0302/arith.jpg?raw=true">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <img style="width:100px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0302/concate.jpg?raw=true"><br/>
    산술 연산자&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    합셩 연산자
</p>

### 내장 함수
&nbsp;&nbsp;* 데이터 값을 간편하게 조작할 수 있다.
&nbsp;&nbsp;&nbsp;&nbsp;* 내장 함수와 사용자 정의 함수로 분류할 수 있다.</br>
&nbsp;&nbsp;&nbsp;&nbsp;* 내용이 많으므로 밑의 사이트 참조 바람.</br>
</br>
```
참조 사이트 : http://www.gurubee.net/lecture/2372
```
</p>

### CASE 표현
&nbsp;&nbsp;* IF-THEN-ELSE 논리와 유사한 방식으로 표현식을 작성해 SQL의 비교 연산 기능을 보완하는 역할을 한다.</br>
</br>
```
SELECT 출력 대상 칼럼 명1
    , CASE
        WHEN 대상 칼럼명 2 > 2000 THEN 대상 칼럼명 2
        ELSE 출력 값
    END AS 새로운 별칭
FROM 출력 대상 칼럼들이 있는 테이블명;
```
<p align="center">
    <img style="width:400px;" src="https://github.com/ERrorASER/CS/blob/yooase12-patch-1/PKH/0302/case.jpg?raw=true"><br/>
    CASE표현 결과
</p>
