섹션 23 SQL 데이터베이스

- How SQL Databases Are Designed & Work
- Defining Data Schemas & Tables
- Querying Data (CRUD Operations)

Stor (and work with) data about restaurants and reviews for these restaurants

- 테이블 (각 테이블마다 행과 열을 가짐)

1. Restaurants : Unique ID, Name, Address, Type
2. Reviews : Unique ID, Reviewer Name, Rating, Text, Date

- Install & set up our SQL database system / software
- Define our tables and their schemas (structre)
- CRUD

  - learn how to insert data into our database tables
  - learn how to read data into from database tables - including filtering etc.
  - learn how to update data in our database tables
  - learn how to delete data in our database tables

- Install & set up our SQL database system / software
- SQL: Strcutre Query Langugage,
- RDMS : Relational Database Management System

- Which one?
  - Open Source : MySQL, PostgreSQL,
  - Commercial License : Microsoft SQL, etc

- mysql 설치

1. 구글에서 mysql 검색
2. 2.4MB 다운로드해서 선택적 설치, 'no thanks. just start my download' 클릭하면 로그인 필요 없음.
   -  https://dev.mysql.com/downloads/file/?id=518834
3. 옵션 선택
   -  Custom - mysql server는 최신 버전으로 선택
   -  application - mysql workbench 최신 버전 선택
   -  2개 선택 후 인스톨 후 전부 default로 설정 및 암호 설정, 윈도우시작 시 서버 실행은 체크해제
4. 윈도우 - 서비스 - mysql을 찾아서 서버 스톱,스타트 가능
5. workbench를 찾아서 실행 후 mysql 로그인

- 데이타베이스 시스템 vs 데이타베이스
  - mySQL은 소프트웨어이고, mySQL server가 실제 데이터베이스, workbench는 도구
  - mySQL server 안에 database가 있고, 그 안에 테이블과 데이터가 존재함.

```sql
-- 레스토랑, 리뷰 실습
-- workbench 왼쪽 하단, schemas 탭에서 데이타베이스(restaurant*finder) 생성 // 소문자와 언더바(*)를 사용함
-- 생성된 데이터베이스의 테이블(restaurants) 생성. // 소문자와 복수형으로 지정.
-- 테이블 엔진은 기본(InnoDB) 설정.
-- 칼럽 설정
-- (name id, datatype INT, PK(고유데이터), AI(자동증가), NL(notNull)
-- (name, varchar(255), NL) -- 레스토랑 이름
-- (type, varchar(255), NL) -- 레스토랑 타입

-- 새 탭을 만들어서 데이터 추가, 탭 메뉴의 번개 아이콘은 쿼리실행
-- INSERT INTO restaurants (name, type) values ('Web Dev Mealery','German')
-- INSERT INTO restaurants (name, type) values ('Pizza House','Italian')
-- INSERT INTO restaurants (name, type) values ('Beergarden','German')

-- 데이터 조회 쿼리
-- SELECT _ FROM restaurant
-- 데이터 조회 조건 쿼리 ( OR, AND, <, >도 사용 가능)
-- SELECT _ FROM restaurant WHERE type = 'German'
-- 특정 열 데이터만 조회
-- SELECT name FROM restaurant WHERE type = 'German'
-- SELECT id, name FROM restaurant WHERE type = 'German'
-- count 함수 사용 조회
-- SELECT COUNT(\*) FROM restaurant WHERE type = 'German'

-- 모든 name 데이터 업데이트
-- UPDATE restaurants SET name = 'Web Dev Meals'
-- 특정 데이터 업데이트
-- UPDATE restaurants SET name = 'Web Dev Meals' WHERE id = 1;

-- 데이터 삭제
-- DELETE FROM restaurants WHERE id = 1; -- 같은 이름이 있을 수 있으므로 id로 삭제 해야 함.
```
```sql
- 새로운 테이블 생성
  테이블 (각자 Unique ID를 가지고 있음)
  'addresses'
  id INT, PK, NN, AI
  street VARCHAR(255), NN
  street_number VARCHAR(45), NN
  city VARCHAR(255), NN
  postal_code INT, NN
  country VARCHAR(255), NN

'types'
id INT, PK, NN, AI
name VARCHAR(100), NN

- restaurants 테이블 구조 변경, 오른쪽 클릭 후 alter table 또는 drop table

* alter table 테이블이 비어있지 않은 경우 기존 데이터 처리가 곤란함.

'restaurants' 테이블 생성, 특정 주소와 유형 연결
id INT, PK, NN, AI
name VARCHAR(255), NN
address_id INT, NN (연결하려는 칼럼과 같아야 함)
하단의 Foreign Keys 탭에서 관계에 대한 자세한 설정 가능함.
type_id INT, NN

'review' 테이블 생성
id INT, PK, NN
reviewer_name VARCHAR(1000), NN
rating INT, NN
text TEXT
date DATETIME, NN,default/Expression : CURRENT_TIMESTAMP --datatype DATE는 날짜만 나옴
restaurant_id INT, NN

-- 데이터 삽입
INSERT INTO types (name) VALUES ('Itallian');
INSERT INTO types (name) VALUES ('German');
INSERT INTO types (name) VALUES ('Austrian');

INSERT INTO addresses (street, street_number, city, postal_code, country) VALUE (
'Teststreet',
'23a',
'Munich',
81541,
'Germany'
);
INSERT INTO addresses (street, street_number, city, postal_code, country) VALUE (
'Greatstreet',
'12',
'Barlin',
10115,
'Germany'
);INSERT INTO addresses (street, street_number, city, postal_code, country) VALUE (
'Greatstreet',
'12',
'Barlin',
10115,
'Germany'
);

INSERT INTO restaurant (name, address_id, type_id) VALUES ('Schnitzelhaus', 1, 3);
INSERT INTO restaurant (name, address_id, type_id) VALUES ('Burgerhouse', 1, 2);
INSERT INTO restaurant (name, address_id, type_id) VALUES ('Le Mama', 2, 1);

INSERT INTO reviews (reviewer_name, rating, text, restaurant_id) VALUES (
'Maximilian Schwarzuller',
4,
'This was asesome!',
2
);

INSERT INTO reviews (reviewer_name, rating, restaurant_id) VALUES (
'Jules Barnes',
2,
2
);

INSERT INTO reviews (reviewer_name, rating, text, restaurant_id) VALUES (
'Jules Barnes',
4,
'This was delicious!'
3
);

INSERT INTO reviews (reviewer_name, rating, text, restaurant_id) VALUES (
'Anna Schulz',
5,
'Amazing'
3
);

-- 데이터 조회
SELECT \* FROM reviews WHERE rating > 3;

-- 쿼리 결합 'JOIN'
-- 'SELECT _ FROM restaurant'의 id들을 활용하여 여러 테이블 데이터 결합시키기
-- 'INNER JOIN ~ ON ~'
SELECT _ FROM restaurants INNER JOIN addresses ON (restaurants.address_id + addresses.id);

-- 조회 필드 제한
SELECT restaurants.name, addresses.\* FROM restaurants
INNER JOIN addresses ON (restaurants.address_id + addresses.id);

-- 여러 테이블 결합
SELECT restaurants.name,addresses.\*, types.name FROM restaurants
INNER JOIN addresses ON (restaurants.address_id + addresses.id)
INNER JOIN types ON restaurants.type_id = types.id;

-- 별칭 할당 'AS'
SELECT restaurants.name,addresses.\*, types.name AS type_name FROM restaurants
INNER JOIN addresses ON (restaurants.address_id + addresses.id)
INNER JOIN types ON restaurants.type_id = types.id;

-- 결합된 쿼리에 조건문 추가 'WHERE'
SELECT restaurants.name,addresses.\*, types.name AS type_name FROM restaurants
INNER JOIN addresses ON (restaurants.address_id + addresses.id)
INNER JOIN types ON restaurants.type_id = types.id
WHERE addresses.city ='Munich';

-- 평점이 3 이상 레스토랑 모든 정보 조회
SELECT \* FROM reviews
INNER JOIN restaurants ON reviews.restaurant_id = restaurants.id
INNER JOIN addresses ON restaurants.address_id = addresses.id
INNER JOIN types ON restaurants.type_id = types.id
WHERE rating > 3;
```

-- 모듈 요악
정규화된 모델로 테이블을 저장하고 링크함.
Relationship in Databases
one to one :

- One record in table A is related to exactly one other record in table B.
- A team has exactly one team leader and that team leader leads exactly one team.
    - one-to-many :
- One record in table A is related to many records in B, each record in B is only related to one record in A
- A restaurant has many reviews but each review is for exactly one restaurant
    - many-to-many :
- One record in table A is related to many records in B, each record in B is also related to many record in A
- A restaurant has many customers and each customer visits many restaurants.
