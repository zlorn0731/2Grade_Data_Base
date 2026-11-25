# 📚 2학년 데이터베이스 (Data Base)
## 09 : SQL기초 및 테이블 생성

### Introduction
- 
| 그림 속 용어 | 실제 역할 |
|--------------|-----------|
| 사용자 | SQL을 입력하는 사용자 |
| 데이터 언어 | DBMS에 요청할 때 쓰는 SQL |
| DBMS | SQL을 받아 처리하는 MySQL 서버 |
| 데이터베이스 | student 테이블 같은 데이터가 저장된 곳 |
| 데이터베이스 관리자(DBA) | 사용자 권한이나 백업 등을 관리하는 사람 |
```text
[예시]

select * from student;

student 테이블의 모든 행과 열을 조회하라는 뜻
Workbench는 SQL을 MySQL 서버에 보내고,
MySQL 서버는 데이터를 찾아 결과를 돌려줌

그 결과를 Workbench 화면에서 확인
```


### 수업 목표
- SQL의 기본과 사용법을 이해하고, SQL로 테이블을 만들 수 있게 되는 것
```sql
create table student (
  sno int primary key,
  name varchar(20)
);

create table student - student라는 테이블을 만듦
sno int primary key - 학번을 정수로 저장하고, 학번으로 학생을 구분
name varchar(20) - 이름을 최대 20자까지 저장
```

### SQL
- Structured Query Language
  - 이름에 Query가 들어가지만, 지금까지 본 것처럼 데이터 조회부터 테이블 생성까지 할 수 있음
- 관계 DBMS에서 데이터를 다루기 위해 설계된 언어
- SEQUEL(Structured English QUEry Language)에서 유래 (1974)
- ANSI(미국 표준 연구소)와 ISO(국제 표준화 기구)에서 관계 데이터베이스 표준언어로 채택
- 주요 상용 DBMS에서 데이터 언어로 채택
- 
| SQL 명령 | student 테이블에서 하는 일 |
|-----------|---------------------------|
| create table | 학생 데이터를 담을 테이블을 만듦 |
| insert | 학생 데이터를 한 행 추가 |
| select | 저장된 학생 데이터를 조회 |
- 종합 데이터베이스 언어 역할
  - 데이터 정의어(DDL)
  - 데이터 조작어(DML)
  - 데이터 제어어(DCL)
- 
| 분류 | 역할 | 대표 명령어 |
|------|------|-------------|
| DDL 데이터 정의어 | 테이블의 구조를 만들거나 바꿈 | create, alter, drop |
| DML 데이터 조작어 | 데이터를 조회하거나 추가, 수정, 삭제 | select, insert, update, delete |
| DCL 데이터 제어어 | 사용자의 접근 권한을 주거나 회수 | grant, revoke |
```text
[drop, delete 구분]

drop table student; - 테이블 자체를 삭제 DDL
delete from student; - 테이블 안의 모든 행을 삭제 DML
```
- 관계대수를 기초로 함
```sql
select name
from student
where grade = 2;

where grade = 2;로 2학년 학생의 행을 고르고, select name으로 이름 열을 가져옴
```
- SQL 표준화
  - 사용 RDBMS 간의 전환 용이
  - 여러 관계 DB를 접근하는 DB 응용 프로그램 작성 지원
- 사용 방식
  - 대화식 SQL(Interactive SQL)
    - 터미널을 통해 명령과 결과 입출력
    - 예시 : MySQL Workbench를 사용하여 SQL 입력, 결과 확인
  - 내포된 SQL(Embedded SQL)
    - 응용 프로그램에 삽입된 형태로 사용
    - 예시 : C/Java/Python 코드 안에 SQL 포함, 실행 결과를 코드에서 처리
```text
대화식 SQL - 네가 MySQL Workbench에서 직접 SQL을 실행하고 결과를 확인하는 방식
내포된 SQL - Java같은 프로그램 코드에 SQL을 넣어 실행하고, 그 결과를 프로그램에서 처리하는 방식

관계 데이터 모델에서 배운 릴레이션, 튜플, 속성은 SQL에서 각각 테이블, 행, 열이라고 부름
```

### 계정 비밀번호 변경
- 아래 내용 중 다음 부분을 자신의 것으로 바꾸어 입력
  - stdt150 : 자신의 계정명으로 변경
  - here : 자신의 새 비밀번호로 변경
```sql
alter user 'stdt150'@'%' identified by 'here';

alter user - 이미 존재하는 MySQL 계정의 설정을 변경
'stdt150'@'%' - 변경할 계정을 지정, stdt150은 사용자 이름이고, %는 접속 호스트
identified by 'here' - 이 계정에 설정할 새 비밀번호를 지정

모든 접속 주로(%)에 대해 계정명 'stdt150'의 비밀번호를 'here'로 변경

alter table은 테이블 구조를 바꿈, alter user는 계정 설정을 바꿈
Workbench에서 이 명령을 실행해 MySQL 계정의 비밀번호를 바꾸면, 다음에 접속할 때 새 비밀번호를 입력
```

## SQL 기초

### DB 생성
- 데이터베이스 구성
  - 데이터 ⊂ 테이블 ⊂ 데이터베이스(스키마)
- 데이터베이스 구축 절차
  - 데이터베이스(스키마) 생성
  - 기본 작업 DB로 생성
  - 테이블 생성
  - 데이터 입력
```sql
[예시]

create database school;
show database;
use school;
```
-
| 명령어 | 하는 일 |
|--------|---------|
| create database schoo; | school 데이터베이스를 새로 만들고 처음에는 테이블 0개 |
| show database; | 데이터베이스 목록을 보여줌, school이 만들어졌는지 확인할 수 있음 |
| use school; | school을 현재 작업할 데이터베이스로 선택 |
```text
create database로 만들고, use로 선택한 뒤, create table로 테이블을 만들면 됨
앞에서 봤던 create table student (...)를 use school; 다음에 실행하면 student 테이블은 school안에 생김
```

### DB 생성 예시
- 순서
  - DB 만들기 → 작업할 DB 선택 → 테이블 만들기 → 데이터 넣기
```sql
create database 1234_library;
use 1234_library;
create table book(...);
insert into book values (100, 'Database');
```
- 
| 명령문 | 하는 일 |
|--------|---------|
| create database 1234_library; | 1234_library라는 데이터베이스를 만듦 |
| use 1234_library; | 1234_library를 지금 작업할 DB로 선택, use practice;랑 같은 역할 |
| create table book(...); | 선택한 DB 안에 book 테이블을 만듦, ...자리에는 열 이름과 자료형을 적어야 실제로 실행 |
| insert into book values (100, 'Database'); | book 테이블에 100과 'Database'가 들어 있는 행 한 줄을 추가 |
```text
예를 들어 book의 첫 번째 열이 도서번호, 두 번째 열이 제목이라면 결과는 이렇다

| 도서번호 |   제목   |
----------------------
|   100   | Database |

create database로 DB를 만들고, use로 그 DB를 선택
그래서 그 다음 줄에서 create table book을 실행하면 1234_library안에 book이 생기는 것
```

### SQL 기본 구조
- 
| 값의 종류 | 적는 방법 | 예시 |
|----------|-----------|-------|
| 문자열 | 작은따옴표로 감싸기 | 'Database System' |
| 숫자 | 그대로 적기 | 1234, -123.45 |
| null | 따옴표 없이 null 적기 | NULL, null |
```text
아까 본 insert into book values (100, 'Database');에서 100은 숫자, 'Database'는 문자열이라 제목에만 따옴표가 붙
```
- 문자열
  - 작은 따음표로 둘러싸서 입력
  - 예시 : 'Database System'
  - 문자열 값에 작은 따옴표가 포함돼 있는 경우
    - 이스케이프 문자 사용 : 'Tom\’s notebook'
    - 두 번 연속 입력 : 'Tom"s notebook'
- 숫자
  - 숫자만 그대로 입력(예시 : 1234, -123.45)
- 널(null) 값
  - 데이터가 없음을 의미하는 널 값은 null로 입력(대소문자 미구분)
- 식별자
  - 데이터베이스/테이블/열/인덱스 이름 : 최대 64자
  - 별칭 이름 : 최대 256자
  - MySQL 예약어나 영어/숫자 이외의 문자가 포함된 식별자는 백틱(backtick) 문자(역따옴표)로 둘러싸서 입력(예시 : '도서관')
- 주석
```sql
create database library; --주석내용 (-- 문자 이후부터 줄 끝까지)
/*
주석내용(여러 줄 가능)
*/
```

### 데이터베이스 생성
- 데이터베이스 생성
```sql
create { database | schema }
  [ if not exists ]
  데이터베이스이름;
```
  - if not exists를 명시하면,
    생성하려는 데이터베이스가 존재하지 않을 때만 생성 시도;
    존재한다면 아무런 일도 발생하지 않음
  - if not exists를 명시하지 않은 경우,
    생성하려는 데이터베이스가 이미 존재하면 에러 발생
```sql
[create database]

create database practice;
이 문장을 실행하면 practice라는 DB가 만들어짐
아까 배운 use practice;는 만들어진 DB를 지금 작업할 DB로 선택하는 명령어
---------------------------------------------------------------------------
[if not exists]

if not exists는 "같은 이름의 DB가 없으면 만들어라"라는 뜻
create database if not exists practice;
```
-
| practice의 상태 | if not exists없이 실행 | if not exists를 붙여서 실행 |
|-----------------|------------------------|----------------------------|
| 아직 없음 | DB 생성 | DB 생성 |
| 아직 있음 | 오류 발생 | 기존 DB를 그대로 두고 넘어감 |

### 기본 작업 DB 지정
- 기본 작업 DB 지정
```sql
use 데이터베이스이름;
```
  - 처음 접속할 때 default schema를 지정하면 그 지정한 DB가 기본 작업 DB로 지정됨
  - 기본 작업 DB로 지정하지 않으면 테이블을 사용할 때마다 [DB명.테이블명]으로 지칭해야 함
```sql
[예시]

방금 만든 practice를 지금 작업할 데이터베이스로 선택
use practice;

이후에는 테이블 이름만 써도 MySQL이 practice안에서 그 테이블을 찾음
use practice;
select * from book;

기본 작업 DB를 선택하지 않은 상태라면, practice.book처럼 'DB이름.테이블이름'으로 위치를 지정
select * from practice.book;
```

### 테이블 생성
- 단순화한 기본 형식
```sql
create table 테이블이름
  ( {열이름 데이터타입}* );
```
```sql
create table 도서(
  번호 int,
  제목 varchar(30),
  가격 int);
```
- 
| 열 이름 | 데이터 타입 | 넣을 수 있는 값의 예시 |
|---------|------------|-------------------------|
| 번호 | int | 정수 [100] |
| 제목 | varchar(30) | 최대 30글자의 문자열 ['데이터베이스 시스템'] |
| 가격 | int | 정수 [25000] |
```text
괄호 안에는 | 열 이름 데이터타입 | 순서로 적음
열과 열 사이는 쉼표로 구분하고, 마지막 열인 가격 int 뒤에는 쉼표가 없음

실행하면 번호, 제목, 가격 이라는 열 3개를 가진 빈 테이블이 생김
표에 적힌 100, '데이터베이스 시스템', 25000은 나중에 insert로 넣을 수 있는 예시 값
```
- 참고 : 테이블 구성 확인
```sql
describe 도서;

테이블의 구조 정보(칼럼 구성) 검색
```
- describe로 열 구성 확인하기
```sql
describe 도서;

방금 만든 도서 테이블에 어떤 열이 있고, 각 열의 데이터 타입이 뭔지 보여줌
결과에는 field는 열 이름, type은 데이터 타입
```

```sql
show create table 도서;

테이블 생성 시 사용된 create table 명령문을 보여줌
```
- show create table로 생성 구문 확인하기

