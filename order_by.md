# order
- 지정된 칼럼을 기준으로 행을 정렬

## 문법

```sql
SELECT * FROM 테이블명 ORDER BY 정렬의 기준으로 사용할 열 [DESC | ASC]
```

- desc : 내림차순
- asc : 올림차순  

## 예제

### 테이블 생성 예제

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
```

### 행 삽입 예제

```sql
INSERT INTO `student` VALUES (2, '박재숙', '남자', '서울',  10, '1985-10-26 00:00:00');
INSERT INTO `student` VALUES (1, '이숙경', '여자', '청주', 200, '1982-11-16 00:00:00');
INSERT INTO `student` VALUES (3, '백태호', '남자', '경주', 350, '1989-2-10 00:00:00');
INSERT INTO `student` VALUES (4, '김경훈', '남자', '제천', 190, '1979-11-4 00:00:00');
INSERT INTO `student` VALUES (8, '김정인', '남자', '대전', 200, '1990-10-1 00:00:00');
INSERT INTO `student` VALUES (6, '김경진', '여자', '제주', 400, '1985-1-1 00:00:00');
INSERT INTO `student` VALUES (7, '박경호', '남자', '영동', 310, '1981-2-3 00');
```

### 행 정렬 예제

```sql
select * from student order by distance desc;
select * from student order by distance desc, address asc;
```

- 밑의 쿼리는 distance와 address를 모두 고려 
- 앞에 있는 컬럼부터 고려
- distance안에서 동일한 데이터가 있는 경우 address를 기준으로 정렬
 
