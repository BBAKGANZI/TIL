``` sql
# if not exists: 없으면 만들어라
USE mcdb;
CREATE TABLE if not exists addr_book (
  `no` INT UNSIGNED NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(10) NOT NULL, 
  tel VARCHAR(14),
  nickname VARCHAR(20) DEFAULT '별명',
  PRIMARY KEY(`no`)
) AUTO_INCREMENT=10001;
DESC addr_book;
```

```sql
# 데이터 삽입
INSERT INTO addr_book(NAME, tel) VALUES
  ('james', '010-2345-6789'), ('maria', '010-3456-7890');
SELECT * FROM addr_book;
```

```sql
show tables;
```

```sql
desc country;
```

```sql
CREATE TABLE tmp(
  id INT PRIMARY KEY,
  col VARCHAR(10)
);
INSERT INTO tmp VALUES(1, '아무개');
SELECT * FROM tmp;
```

```sql
# 테이블 삭제 tmp가 삭제 됨(삭제되면 복구되지 않음)
DROP TABLE tmp;
SHOW TABLES;
```

```sql
# 테이블명 바꾸기
RENAME TABLE addr_book TO address_book;
SHOW TABLES;
```

```sql
# 테이블 변경(컬럼 추가)
ALTER TABLE address_book ADD gender CHAR(4) NOT NULL;
DESC address_book;
```

```sql
ALTER TABLE address_book ADD email VARCHAR(20) AFTER tel;
DESC address_book;
```

```sql
# 테이블 삭제(컬럼 삭제)
ALTER TABLE address_book DROP gender;
DESC address_book;
```

```sql
CREATE TABLE girl_group ( 
  gid INT PRIMARY KEY AUTO_INCREMENT, 
  NAME VARCHAR(32) NOT NULL, 
  debut DATE NOT NULL, 
  hit_song_id INT 
) AUTO_INCREMENT=1001;
```

```sql
CREATE TABLE song ( 
  sid INT PRIMARY KEY AUTO_INCREMENT, 
  title VARCHAR(32) NOT NULL, 
  lyrics VARCHAR(32) 
)AUTO_INCREMENT=101;

show tables;
```

```sql
INSERT INTO song (title, lyrics) 
VALUES ('Tell Me', 'tell me tell me tetetete tel me'),
  ('Gee', 'GEE GEE GEE GEE GEE BABY BABY'),
  ('미스터', '이름이 뭐야 미스터'), 
  ('Abracadabra', '이러다 미쳐 내가 여리여리'),
  ('8282', 'Give me a call Baby baby'), ('기대해', '기대해'),
  ('I Don\'t care', '다른 여자들의 다리를'), 
  ('Bad Girl Good Girl', '앞에선 한 마디 말도'), ('피노키오', '뉴예삐오'),
  ('별빛달빛', '너는 내 별빛 내 마음의 별빛'), 
  ('A', 'A 워오우 워오우워 우우우'),
  ('나혼자', '나 혼자 밥을 먹고 나 혼자 영화 보고'), ('LUV', '설레이나요 '),
  ('짧은치마', '짧은 치마를 입고 내가 길을 걸으면'),
  ('위아래', '위 아래 위위 아래'), ('Dumb Dumb', '너 땜에 하루종일');
  
SELECT * FROM song;
```

```sql
INSERT INTO girl_group (name, debut) 
VALUES ('원더걸스', '2007-02-10'),
  ('소녀시대', '2007-08-02'), ('카라', '2009-07-30'),
  ('브라운아이드걸스', '2008-01-17'), ('다비치', '2009-02-27'),
  ('2NE1', '2009-07-08'), ('f(x)', '2011-04-20'),
  ('시크릿', '2011-01-06'), ('레인보우', '2010-08-12'),
  ('애프터 스쿨', '2009-11-25'), ('포미닛', '2009-08-28');

SELECT * FROM girl_group;
```

```sql
# truncate 테이블의 구조는 남아 있으나 모든 데이터 삭제
TRUNCATE TABLE girl_group;
SELECT * FROM girl_group;
```

```sql
INSERT INTO girl_group (name, debut, hit_song_id) 
        VALUES ('원더걸스', '2007-02-10', 101),
        ('소녀시대', '2007-08-02', 102), ('카라', '2009-07-30', 103),
        ('브라운아이드걸스', '2008-01-17', 104), ('다비치', '2009-02-27', 105),
        ('2NE1', '2009-07-08', 107), ('f(x)', '2011-04-20', 109),
        ('시크릿', '2011-01-06', 110), ('레인보우', '2010-08-12', 114),
        ('애프터 스쿨', '2009-11-25', 113), ('포미닛', '2009-08-28', 108);
SELECT * FROM girl_group;
```

```sql
UPDATE girl_group SET hit_song_id = 201 WHERE gid = 10;
UPDATE girl_group SET hit_song_id = 202 WHERE gid = 11;
```

```sql
# 두 테이블의 공통 부분만 검색
SELECT gg.NAME, gg.debut, s.title
  FROM girl_group AS gg
  JOIN song AS s
  ON gg.hit_song_id = s.sid;
```

```sql
# left outer 타이틀 없는것까지 검색됨
SELECT gg.NAME, gg.debut, s.title
  FROM girl_group AS gg
  left outer JOIN song AS s
  ON gg.hit_song_id = s.sid;
```

```sql
# full outer join 양 테이블 모두 타이틀 없는것까지 검색
SELECT gg.NAME, gg.debut, s.title
  FROM girl_group AS gg
  left outer JOIN song AS s
  ON gg.hit_song_id = s.sid
union
SELECT gg.NAME, gg.debut, s.title
  FROM girl_group AS gg
  right outer JOIN song AS s
  ON gg.hit_song_id = s.sid;
```

```sql
# 2009년도에 데뷔한 걸그룹 정보를 조회
SELECT * FROM girl_group
  WHERE debut BETWEEN '2009-01-01' AND '2009-12-31'
  ORDER BY debut;
```

```sql
# 2009년도에 데뷔한 걸그룹의 히트송은?
SELECT NAME, debut, title
  FROM girl_group
  JOIN song
  ON girl_group.hit_song_id = song.sid
  WHERE debut BETWEEN '2009-01-01' AND '2009-12-31'
  ORDER BY debut;
```

```sql
# 테이블 생성
create table if not exists users (
  uid varchar(20) not null primary KEY,
  pwd char(44) not NULL,
  uname varchar(20) not NULL,
  reg_date datetime default CURRENT_TIMESTAMP,
  is_deleted int default 0
);
DESC users;
```

```sql
# 데이터 추가
ALTER TABLE users ADD COLUMN email varchar(40);
```

```sql
# 테이블 삭제
DROP TABLE users;
```

colab에서 테이블생성

```sql
# 데이터 추가
INSERT INTO users(uid, pwd, uname) VALUES('admin', '1234', '관리자');
select * FROM users;
```

```sql
# 데이터 삭제
TRUNCATE TABLE users;
```

colab에서 데이터 추가

```sql
# 입력한 순서대로 출력
SELECT * FROM users ORDER BY reg_date;
```

```sql
UPDATE users SET is_deleted=1 WHERE uid IN ('gdhong2', 'jbpark2');
SELECT * FROM users ORDER BY reg_date;
```

```sql
# 사용자를 확인할때 is_deleted=0인 데이터에서 등록 시간이 년-월-일 시:분 까지 출력
SELECT uid, uname, email,
  DATE_FORMAT(reg_date, "%Y-%m-%d %H:%i") AS reg_date
  FROM users WHERE IS_deleted = 0 ORDER BY reg_date;
```

```sql
SELECT uid, uname, email,
  DATE_FORMAT(reg_date, "%Y-%m-%d %H:%i") AS reg_date
  FROM users WHERE IS_deleted = 0 AND uid='eskim';
```

```sql
# pwd가 암호화로 출력
SELECT * FROM users ORDER BY reg_date;
```

