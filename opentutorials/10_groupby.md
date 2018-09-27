
# group by
- 특정 칼럼을 기준으로 데이터를 그룹핑함

```sql
SELECT * FROM 테이블명 GROUP BY 그룹핑 할 기준 칼럼명
```

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
INSERT INTO `student` VALUES (2, '박재숙', '남자', '서울',  10, '1985-10-26 00:00:00');
INSERT INTO `student` VALUES (1, '이숙경', '여자', '청주', 200, '1982-11-16 00:00:00');
INSERT INTO `student` VALUES (3, '백태호', '남자', '경주', 350, '1989-2-10 00:00:00');
INSERT INTO `student` VALUES (4, '김경훈', '남자', '제천', 190, '1979-11-4 00:00:00');
INSERT INTO `student` VALUES (8, '김정인', '남자', '대전', 200, '1990-10-1 00:00:00');
INSERT INTO `student` VALUES (6, '김경진', '여자', '제주', 400, '1985-1-1 00:00:00');
INSERT INTO `student` VALUES (7, '박경호', '남자', '영동', 310, '1981-2-3 00');
```

```sql
select sex from student group by sex;
```

* student 테이블에서 sex 값만을 가져와라
* group by의 인자로 sex를 준 것
* 성을 기준으로 출력
 
```sql
select sex,sum(distance), avg(distance) from student group by sex;
```

* sex, sum, avg의 컬럼을 보여줌 
* sex로 그룹핑된 집단들의 sum, avg
* 특정 컬럼으로 기준이 되고 다른 컬럼들의 평균이나 합계를 낼 수 있음
