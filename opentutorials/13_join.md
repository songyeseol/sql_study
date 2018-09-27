# 여러개의 테이블 사용하기

데이터의 규모가 커지면서 하나의 테이블로 정보를 수용하기가 어려워지면 테이블을 분할하고 테이블 간의 관계성을 부여함

## 예제
```sql
DROP TABLE IF EXISTS `student`;
CREATE TABLE `student` (
 `id` tinyint(4) NOT NULL,
 `name` char(4) NOT NULL,
 `sex` enum('남자','여자') NOT NULL,
 `address` varchar(50) NOT NULL,
 `distance` INT NOT NULL,
 `birthday` datetime NOT NULL,
 PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
 
INSERT INTO `student` VALUES (2, '박재숙', '남자', '서울',  10, '1985-10-26 00:00:00');
INSERT INTO `student` VALUES (1, '이숙경', '여자', '청주', 200, '1982-11-16 00:00:00');
INSERT INTO `student` VALUES (3, '백태호', '남자', '경주', 350, '1989-2-10 00:00:00');
INSERT INTO `student` VALUES (4, '김경훈', '남자', '제천', 190, '1979-11-4 00:00:00');
INSERT INTO `student` VALUES (8, '김정인', '남자', '제주', 400, '1990-10-1 00:00:00');
INSERT INTO `student` VALUES (6, '김경진', '여자', '제주', 400, '1985-1-1 00:00:00');
INSERT INTO `student` VALUES (7, '박경호', '남자', '영동', 310, '1981-2-3 00:00:00');
```

위의 예제 중 address는 distance와 관련되어 있기 때문에 location이라는 별도의 테이블로 분할할 수 있음

```sql
DROP TABLE IF EXISTS `student`;
CREATE TABLE `student` (
 `id` tinyint(4) NOT NULL,
 `name` char(4) NOT NULL,
 `sex` enum('남자','여자') NOT NULL,
 `location_id` tinyint(4) NOT NULL,
 `birthday` datetime NOT NULL,
 PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

DROP TABLE IF EXISTS `location`;
CREATE TABLE `location` (
`id`  tinyint UNSIGNED NOT NULL AUTO_INCREMENT ,
`name`  varchar(20) NOT NULL ,
`distance`  tinyint UNSIGNED NOT NULL ,
PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
INSERT INTO `location` VALUES (1, '서울', 10);
INSERT INTO `location` VALUES (2, '청주', 200);
INSERT INTO `location` VALUES (3, '경주', 255);
INSERT INTO `location` VALUES (4, '제천', 190);
INSERT INTO `location` VALUES (5, '대전', 200);
INSERT INTO `location` VALUES (6, '제주', 255);
INSERT INTO `location` VALUES (7, '영동', 255);
INSERT INTO `location` VALUES (8, '광주', 255);
INSERT INTO `student` VALUES (1, '이숙경', '여자', 1, '1982-11-16 00:00:00');
INSERT INTO `student` VALUES (2, '박재숙', '남자', 2, '1985-10-26 00:00:00');
INSERT INTO `student` VALUES (3, '백태호', '남자', 3, '1989-2-10 00:00:00');
INSERT INTO `student` VALUES (4, '김경훈', '남자', 4, '1979-11-4 00:00:00');
INSERT INTO `student` VALUES (6, '김경진', '여자', 5, '1985-1-1 00:00:00');
INSERT INTO `student` VALUES (7, '박경호', '남자', 6, '1981-2-3 00:00:00');
INSERT INTO `student` VALUES (8, '김정인', '남자', 5, '1990-10-1 00:00:00');
```

## join

테이블간의 관계성에 따라서 복수의 테이블을 결합
하나의 테이블인 것처럼 결과 출력

## join의 종류

### outer join

- 매칭되는 행이 없어도 결과를 가져오고 null로 표시한다
- left join / right join

#### left join
```sql
SELECT s.name, s.location_id, l.name AS address, l.distance  FROM student AS s LEFT JOIN location AS l ON s.location_id = l.id;
```

AS
l.name을 address로 표시해라
student라는 테이블에 s라는 별명을 붙인 것
location 테이블에 l이라는 별명을 붙인 것
쿼리를 간결하게 만들기 위함
A LEFT JOIN B
A에다가 B를 조인
ON
student의 location_id컬럼과 location의 id가 같다라는 의미

### inner join
조인하는 두개의 테이블 모두에 데이터가 존재하는 행에 대해서만 결과 가져옴

### inner join과 outer join의 차이

```sql
DELETE FROM location WHERE name='제주';

SELECT s.name, s.location_id, l.name AS address, l.distance  FROM student AS s LEFT JOIN location AS l ON s.location_id = l.id;

SELECT s.name, s.location_id, l.name AS address, l.distance  FROM student AS s INNER JOIN location AS l ON s.location_id = l.id;
```

- left join은 박경호(name=제주)에 대해 null을 출력 / inner join은 생략
- inner join은 조인한 대상 중 하나라도 데이터가 없다면 그 값을 가져오지 않음

