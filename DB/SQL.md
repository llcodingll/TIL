## RDB
- Table : 실제 데이터 저장소
- 데이터를 table 단위로 관리
  - 하나의 record는 여러 attribute를 가짐
  - 데이터 중복 최소화
  - table 간 관계 이용해 필요한 데이터 검색
#### RDB 구조
- Schema : 자료 구조, 표현 방법, 관계 등 전반적 명세
- Table
  - column(attribute)
  - row(record)
  - PK
#### SQL


: 데이터 조장 && 데이터 정의
- 데이터 조회/삽입/삭제/수정
- Object 생성/변경/삭제
- 사용자 생성/삭제/권한 제어

---
### 자료형
| 자료형       | 데이터 유형                                                                                                                                                                                                |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 숫자 자료형    | BIT(M), TINYINT(M), BOOL, BOOLEAN, SMALLINT(M), MEDIUMINT(M), INT(M), INTEGER(M), BIGINT(M)<br/> DOUBLE(M, D), DOUBLE PRECISION(M, D), FLOAT(P), DECIMAL(M, D), DEC(M, D), NUMERIC(M, D), FIXED(M, D) |
| 문자 자료형    | CHAR(M), VARCHAR(M), TINYTEXT(M), TEXT(M), MEDIUMTEXT(M), LONGTEXT(M), ENUM('value1', 'value2', ...), SET('value1', 'value2', ...)                                                                    |
| 날짜 자료형    | DATE, TIME, DATETIME, TIMESTAMP(M), YEAR(4)                                                                                                                                                           |
| BINARY 타입 | BINARY(M), VARBINARY(M)                                                                                                                                                                               |
| BLOB 타입   | TINYBLOB(M), BLOB(M), MEDIUMBLOB(M), LONGBLOB(M)                                                                                                                                                      |

---
## DDL(Data Definition Language)
- `CREATE DATABASE`: 새 데이터 베이스 생성
- 1 DB 여러 table
- DB 생성 시, 관리자 권한으로 생성
- `SHOW DATABASES`: DB 목록 확인
- `DROP {DATAVBASE|SCHEMA} IF EXISTS dbName`: DB 삭제
  - 삭제 시, DROP DATABASE 권한 필요
- `USE dbName`: (접근 권한이 있는 경우) DB 사용
- Character set 설정
  - DB 생성 시 설정 || 생성 후 수정
  - 문자집합: 각 문자가 컴퓨터에 저장될 때 어떤 '코드'로 저장되는지 규칙 지정한 집합
  - Collation: 특정 문자 집합에 의해 DB에 저장된 값들 비교/검색/정렬, ...(비교 규칙 집합)
- `CREATE TABLE tableName`: table 생성
  - 컬럼명, 데이터 타입 지정, 제약 조건 추가
- `DESCRIBE|DESC tableName`: 생성된 table schema 확인
---
### Constraint(제약 조건)
- 컬럼에 저장될 데이터 조건
- 제약 조건에 위배되는 데이터 저장 불가
- table 생성 시 컬럼에 지정 || constraint로 지정(`ALTER` 사용)

| 제약 사항       | 설명                                                                            |
|-------------|-------------------------------------------------------------------------------|
| NOT NULL    | 각 행은 해당 열의 값 포함<br/>NULL 허용 X                                                 |
| UNIQUE      | 컬럼에 중복된 값 저장 X, NULL 값 허용                                                     |
| PRIMARY KEY | 기본키, 컴럼에 중복된 값 저장 X, NULL 값 X<br/>record 구분을 위한 유일한 값                         |
| FOREIGN KEY | 특정 테이블의 PK 컬럼에 저장된 값만 저장<br/>참조키=외래키<br/>NULL 값 허용<br/>어떤 컬럼에 어떤 데이터 참조하는지 지정 |
| DEFAULT     | record 입력 시, 해당 열의 값이 입력되지 않으면 넣어줄 값 지정                                       |
| CHECK       | 값의 범위/종류 지정<br/>MYSQL 8부터 사용 가능                                               |
---
## DML(Data Manipulation Language)
### INSERT
- 생성 시 작성한 모든 컬럼에 입력 갑 주어지면 컬럼 이름 생략 가능
- 컬럼 이름과 입력 값 순서 일치하도록 작성(NULL, DEFAULT, AUTO INCREMENT)
- `INSERT INTO tableName (~~) VALUES (~~);` 
### UPDATE
- 기존 record 수정
- WHERE절 이용해 하나 이상의 record 수정 가능
  - 생략하면 table의 모든 행 수정
- `UPDATE tableName SET colName=value, ~~~ WHERE whereCondition;`
### DELETE
- 기존 record 삭제
- WHERE절 이용해 하나 이상의 record 삭제 가능
- `DELETE FROM tableName WHERE whereCondition;`

---
## MySQL Functions
---
## Transaction


: Commit하거나 Rollback 할 수 있는 가장 작은 작업 단위
- Commit: transaction을 종료해 변경 사항에 대해 영구적으로 저장
- Rollback: transaction에 의해 수행된 모든 변경 사항 실행 취소
* MySQL에서는 기본이 AUTO COMMIT됨
* 