# SELECT
 
- 테이블에서 데이터를 조회

## 문법

```sql
SELECT 칼럼명1, 칼럼명2
    [FROM 테이블명]
    [GROUP BY 칼럼명]
    [ORDER BY 칼럼명 [ASC | DESC]]
    [LIMIT offset, 조회 할 행의 수] 
```

- 부분적으로 조회하고 싶다면 컬럼명 기재, 아니라면 별표 *
- 대괄호는 생략가능 
- 기술되어있는 순서대로 명령 
- 무조건 from, group by, order by, limit 순서

## 예제

### 예제를 위한 테이블 생성 

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
INSERT INTO `student` VALUES (2, '박재숙', '남자', '서울', '1985-10-26 00:00:00');
INSERT INTO `student` VALUES (1, '이숙경', '여자', '청주', '1982-11-16 00:00:00');
INSERT INTO `student` VALUES (3, '백태호', '남자', '경주', '1989-2-10 00:00:00');
INSERT INTO `student` VALUES (4, '김경훈', '남자', '제천', '1979-11-4 00:00:00');
INSERT INTO `student` VALUES (8, '김정인', '남자', '대전', '1990-10-1 00:00:00');
INSERT INTO `student` VALUES (6, '김경진', '여자', '제주', '1985-1-1 00:00:00');
INSERT INTO `student` VALUES (7, '박경호', '남자', '영동', '1981-2-3 00:00:00');
```

### 조회

```sql
SELECT * FROM student; 
```

- student 테이블의 모든 컬럼을 조회

```sql
SELECT name, birthday FROM student; 
```
- student 테이블의 name, birthday만 조회

```sql
SELECT * FROM student WHERE id=3; 
```
- 모든 컬럼을 가져오되 id값으로 3을 갖는 행에 대해서만 조회

```sql
SELECT * FROM student WHERE sex='남자' AND address='서울'; 
```
-sex로 '남자', address로 '서울' 값을 가지는 사람을 조회

```sql
SELECT * FROM student WHERE sex='여자' OR address='서울'; 
```
- 두 조건 중 하나만 충족해도 조회
- 여자이거나 서울사는 사람 조회
- 조건을 좀더 디테일하게 설정 

```sql
SELECT * FROM student LIMIT 3; 
```
- 조회한 결과를 몇개를 가져올 것인지 지정
- 행을 3개만 가져와라
- 행이 100만건이 존재할 경우 전체 조회하면 시스템에 막대한 영향을 줄 수 있음

```sql
SELECT * FROM student LIMIT 1,1; 
```
- 리밋 뒤 첫번째 숫자 = offset
- 두번째 숫자 = rowcount
- indexing할 때 첫번째 행이 0이 되고 두번째 행이 1
- 즉, 2번째 행(offset=1)에서 한 개(rowcount=1)의 행만 출력

```sql
SELECT * FROM student LIMIT 2,1; 
```
- 즉, 3번째 행에서 한 개의 행만 출력

```sql
SELECT * FROM student LIMIT 3,1;
```
- 즉, 4번째 행에서 한 개의 행만 출력 

```sql
SELECT * FROM student WHERE sex='남자' LIMIT 2; 
```
- 성이 남자인 사람들의 리스트에서 두 개의 행만 출력 

 
