# DELETE / DROP / TRUNCATE

## 문법

```sql
DELETE FROM 테이블명 [WHERE 삭제하려는 칼럼 명=값]
```

## 예제

### 예제용 table 새로 만들기 

```sql
DROP TABLE IF EXISTS `student`;
CREATE TABLE `student` (
  `id` tinyint(4) NOT NULL,
  `name` char(4) NOT NULL,
  `sex` enum('남자','여자') NOT NULL,
  `address` varchar(50) NOT NULL,
  `birthday` datetime NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
INSERT INTO `student` VALUES (1, '이숙경', '여자', '청주', '1982-11-16 00:00:00');
INSERT INTO `student` VALUES (2, '박재숙', '남자', '서울', '1985-10-26 00:00:00');
INSERT INTO `student` VALUES (3, '백태호', '남자', '경주', '1989-2-10 00:00:00');
INSERT INTO `student` VALUES (4, '김경훈', '남자', '제천', '1979-11-4 00:00:00');
INSERT INTO `student` VALUES (8, '김정인', '남자', '대전', '1990-10-1 00:00:00');
INSERT INTO `student` VALUES (6, '김경진', '여자', '제주', '1985-1-1 00:00:00');
INSERT INTO `student` VALUES (7, '박경호', '남자', '영동', '1981-2-3 00:00:00';
```

### 1) DELETE

```sql
DELETE FROM student WHERE id = 2;
```

- 아이디 값이 2인 행만을 삭제 
- WHERE을 빼면 테이블의 모든 것이 삭제 됨 **조심


### 2) TRUNCATE

```sql
TRUNCATE student;
```

- 테이블의 전체 데이터를 삭제
- 테이블에 외부키(foreign key)가 없다면 DELETE보다 훨씬 빠르게 삭제됨
- delete는 행단위로 삭제되기에 truncate가 훨씬 빠름 

### 3) DROP

```sql
DROP TABLE student;
```

- 아예 테이블을 데이터베이스에서 삭제

### 주의사항
- delete, truncate, drop table은 신중하게
- 항상 백업하는 것이 중요
