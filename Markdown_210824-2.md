```sql
use mcdb;
```

```sql
create table city like world.city;
desc city;
```

```sql
insert into city select * from world.city;
select * from city limit 10;
```

```sql
create table country like world.country;
insert into country select * from world.country;
select * from country limit 10;
```

```sql
create table countrylanguage like world.countrylanguage;
insert into countrylanguage select * from world.countrylanguage;
select * from countrylanguage limit 10;
```

```sql
show tables;
```

```sql
select * from city;
```

```sql
select * from city whrere CountryCode='KOR';
```

```sql
SELECT * FROM city WHERE District='Kyonggi'
```

```sql
# name과 population만 출력
SELECT NAME, population FROM city WHERE District='Kyonggi'
```

```sql
# ` ` (물결로 이름 구분)
SELECT `NAME`, population FROM city WHERE District='Kyonggi'
```

```sql
# 필드명 이름이 바뀜
SELECT `NAME` AS city_name, population AS pop FROM city WHERE District='Kyonggi'
```

```sql
# 경기에서 50만이상
SELECT * FROM city 
	WHERE District='Kyonggi' AND population>500000;
```

```sql
# and, or, not 사용 가능
SELECT * FROM city 
	WHERE District='Kyonggi' AND (not population>500000);
```

```sql
# 시가 중복되어 나옴
SELECT district FROM city WHERE countrycode='KOR';
```

```sql
# 시가 중복되지 않고 출력
SELECT distinct district FROM city WHERE countrycode='KOR';
```

```sql
# 데이터베이스 앞 테이블명(내 데이터가 아닌)
SELECT * FROM world.city WHERE countrycode='KOR';
```

```sql
SELECT * FROM city WHERE district='Taejon';
```

```sql
SELECT DISTINCT district FROM city WHERE countrycode='KOR';
```

```sql
SELECT * FROM city
  WHERE district IN ('Taejon', 'Chungchongnam', 'Chungchongbuk');
```

```sql
SELECT * FROM city WHERE 
countrycode='kor' AND population>1000000 and population%2=0;
```

```sql
SELECT * FROM city WHERE 
countrycode='kor' AND population>1000000 and population<2000000;
```

```sql
SELECT * FROM city WHERE 
countrycode='kor' AND population betweeen 1000000 and 2000000;
```

```sql
# tae% -> tae 이하 모두
select * from city where countrycode='kor' AND `name` like 'tae%';
```

```sql
# _ -> 임의의 한글자를 모를때
select * from city where countrycode='kor' AND `name` like 't_e%';
```

```sql
# population의 오름차순으로 나옴
select * from city where district='Kyonggi' ORDER BY population;
```

```sql
# population의 숫자가 많은 순으로 정렬
select * from city where district='Kyonggi' ORDER BY population desc;
```

```sql
# 필드명이 여러개 올 수 있음
select * from city where countrycode='KOR'
  ORDER BY district, population;
```

```sql
select * from city where countrycode='KOR'
  ORDER BY district desc, population desc;
```

```sql
SELECT COUNT(*) FROM city WHERE countrycode='KOR';
```

```sql
# 합계, 평균
SELECT sum(population), AVG(population) FROM city WHERE countrycode='KOR';
```

```sql
# 최소, 최대 값
SELECT min(population), max(population) FROM city WHERE countrycode='KOR';
```

```sql
SELECT min(population) AS min_pop, max(population) FROM city WHERE countrycode='KOR';
```

```sql
# city쭉 나열
SELECT GROUP_CONCAT(NAME) FROM city WHERE countrycode='KOR';
```

```sql
# 시, 광역시 갯수
SELECT district, COUNT(*) 
  FROM city 
  WHERE countrycode='KOR'
  GROUP BY district;
```

```sql
# having은 group by에 걸려있는 조건문
SELECT district, COUNT(*) 
  FROM city 
  WHERE countrycode='KOR'
  GROUP BY district
  HAVING COUNT(*)=6;
```

```sql
SELECT countrycode, COUNT(*) 
  FROM city 
  GROUP BY countrycode
  HAVING COUNT(*)>50
  ORDER BY COUNT(*) desc;
```

```sql
SELECT countrycode, COUNT(*) 
  FROM city 
  GROUP BY countrycode
  HAVING COUNT(*)>50
  ORDER BY COUNT(*) desc
```

```sql
# 상위 5개 건너뛰고(offset) 5개 출력(limit)
SELECT countrycode, COUNT(*) 
  FROM city 
  GROUP BY countrycode
  HAVING COUNT(*)>50
  ORDER BY COUNT(*) desc
  LIMIT 5 OFFSET 5;		
```

```sql
SELECT country.name, COUNT(city.name)
  FROM city
  INNER JOIN country
  ON city.CountryCode=country.code
  GROUP BY city.countrycode
  ORDER BY COUNT(*) desc
  LIMIT 10 OFFSET 10;
```

```sql
# 위와 같은 결과 값
SELECT r.name, COUNT(l.Name)
  FROM city AS l
  JOIN country AS r
  ON l.CountryCode=r.code
  GROUP BY l.countrycode
  ORDER BY COUNT(l.name) desc
  LIMIT 10 OFFSET 0;
```

```sql
# 국가명, 도시명, 도시인구수 Top10
SELECT r.name AS '국가명', l.name AS '도시', l.population
  FROM city AS l
  JOIN country AS r
  ON l.CountryCode=r.code
  ORDER BY l.population desc
  LIMIT 10 OFFSET 0;
```

```sql
SELECT * FROM city WHERE countrycode='KOR';
```

```sql
# district 이름 바꾸기
UPDATE city SET district='경기' WHERE district='Kyonggi';
SELECT * FROM city WHERE district='경기';
UPDATE city SET district='강원' WHERE district='Kang-won';
SELECT * FROM city WHERE district='강원';
```

```sql
# data 값 바꾸기
UPDATE city SET district='서울', population=10000000
 WHERE district='Seoul';
SELECT * FROM city WHERE district='서울';
```

```sql
SELECT DISTINCT district FROM city WHERE countrycode='KOR';
```

```sql
# district 이름 바꾸기
UPDATE city SET district='인천' WHERE district='Inchon';
UPDATE city SET district='대구' WHERE district='Taegu';
UPDATE city SET district='대전' WHERE district='Taejon';
UPDATE city SET district='광주' WHERE district='Kwangju';
UPDATE city SET district='경남' WHERE district='Kyongsangnam';
UPDATE city SET district='전북' WHERE district='Chollabuk';
UPDATE city SET district='충북' WHERE district='Chungchongbuk';
UPDATE city SET district='경북' WHERE district='Kyongsangbuk';
UPDATE city SET district='충남' WHERE district='Chungchongnam';
UPDATE city SET district='제주' WHERE district='Cheju';
UPDATE city SET district='전남' WHERE district='Chollanam';
SELECT DISTINCT district FROM city WHERE countrycode='KOR';
```

```sql
SELECT * FROM city WHERE district='경기';
```

```sql
INSERT INTO city(id, NAME, countrycode, district, population)
  VALUES(default, '김포', 'KOR', '경기', 200000);
SELECT * FROM city WHERE district='경기'
```

```sql
INSERT INTO city(NAME, countrycode, district, population)
  VALUES('화성', 'KOR', '경기', 300000);
SELECT * FROM city WHERE district='경기';
```

```sql
INSERT INTO city
  VALUES
  (DEFAULT, '오산', 'KOR', '경기', 150000),
  (DEFAULT, '포천', 'KOR', '경기', 120000);
SELECT * FROM city WHERE district='경기' ORDER BY id DESC LIMIT 5;
```

```sql
DELETE FROM city WHERE id=4082;
SELECT * FROM city WHERE district='경기' ORDER BY id DESC LIMIT 5;
```

```sql
CREATE TABLE koreancity LIKE city;
DESC koreancity;
```

```sql
insert into koreancity select * from city where countrycode='KOR';
select * from koreancity;
```

```sql
delete from city where id>4080;
select * from city order by id desc limit 3;
```

```sql
CREATE VIEW largecity AS SELECT * FROM city
  WHERE population>7000000;
```

```sql
SELECT * FROM largecity;
```

```sql
SHOW TABLES;
```

```sql
SELECT district, AVG(population) FROM koreancity GROUP BY district;
```

```sql
SELECT district, NAME, population FROM koreancity AS c1
  WHERE population >
  (SELECT AVG(population) FROM koreancity AS c2
  WHERE c1,district = c2.district GROUP BY district);
```

```sql
# 대륙별로 국가숫자, GNP의 합, 평균 국가별 GNP는?
SELECT continent AS '대륙', COUNT(*) AS '국가숫자',
  sum(gnp) as 'gnp의 합', ROUND(AVG(gnp),2) AS '평균 국가별 gnp'
  FROM country
  GROUP BY continent;
```

```sql
desc country;
```

```sql
# 아시아 대륙에서 인구가 가장 많은 도시 10개를 내림차순으로 보여줄 것
# (대륙명, 국가명, 도시명, 인구수)

SELECT l.continent, l.name AS countryname,
       r.name AS cityname, r.population
  FROM country AS l
  JOIN city AS r
  ON l.code = r.countrycode
  WHERE l.Continent='Asia'
  ORDER BY r.population desc
  LIMIT 10;
```

```sql
# 전 세계에서 인구가 가장 많은 10개 도시에서 사용하는 공식언어는?

SELECT l.name AS '도시', l.population AS '인구', r.language AS '언어'
  FROM city AS l
  JOIN countrylanguage AS r
  ON l.CountryCode=r.CountryCode
  WHERE r.isofficial='T'
  ORDER BY l.population desc
  LIMIT 10;
```

```sql
CREATE TABLE date_table (
  id INT AUTO_INCREMENT PRIMARY KEY,
  dt DATETIME DEFAULT current_timestamp
);
DESC date_table;
```

```sql
INSERT INTO date_table (dt) VALUES
  ('2017-08-28 17:22:21'), ('2017-02-15 10:22:24'),
  ('2017-12-09 22:13:24'), ('2018-07-06 20:15:18');
SELECT * FROM date_table;
```

```sql
INSERT INTO date_table VALUES (DEFAULT, DEFAULT);
SELECT * FROM date_table;
```

```sql
SELECT date_format(dt, '%Y-%m-%d') AS my_date,		# 년 월 일
       DATE_FORMAT(dt, '%h:%i:%s %p') AS my_time 	# 시 분 초 pm/am(대문자 H면 24시간제)
		 FROM date_table;
```

```sql
SELECT date_format(dt, '%Y-%m-%d') AS my_date,
       DATE_FORMAT(dt, '%h:%i:%s %p') AS my_time,
		 DATE_FORMAT(dt, '%r') AS my_time2	# 위에것과 같은 값
		 FROM date_table;
```

```sql
SELECT NOW(), CURDATE(), CURTIME();
```

```sql
SELECT DATE_ADD(NOW(), INTERVAL 2 MONTH);	# 2달 후
```

```sql
SELECT DATE_ADD(NOW(), INTERVAL 5 day);		# 5일 후
```

```sql
SELECT to_days(CURDATE());			# 서기 0년부터
```

```sql
SELECT TO_DAYS('2021-11-18') - TO_DAYS(NOW());	# d-day counter
```

```sql
SELECT DAYOFWEEK(dt) FROM date_table;		# 1-일요일
```

