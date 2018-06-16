# UPDATE SET 

## 문법

```sql
UPDATE 테이블명 SET 컬럼1=컬럼1의 값, 컬럼2=컬럼2의 값 WHERE 대상이 될 컬럼명=컬럼의 값
```

- 여러 컬럼을 변경하려면 comma 삽입 


## 예제

### 예제를 위한 새로운 student 테이블 만들기 

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
INSERT INTO `student` VALUES (7, '박경호', '남자', '영동', '1981-2-3 00:00:00');
```

#### 만약 한글 깨진다면

```sql
set character set euckr;
```
하고 다시 drop & create

### 데이터 변경

```sql
UPDATE `student` SET address='서울';
```

- address 열의 값을 '서울'로 모두 변경하는 명령

```sql
UPDATE `student` SET name='이진경' WHERE id=1;
```

- where은 어떤 행에 적용될 것인가 지정
- id 열 값이 1인 행에 대하여 앞의 명령을 실행 

```sql
UPDATE `student` SET name='이고잉', birthday='2001-4-1' WHERE id=3;
```

- 두 컬럼 동시 변경

## 헷갈리는 부분

### 데이터베이스 모두 보고 싶을 때
```sql
SHOW DATABASES;
```

### 테이블 모두 보고싶을 때
```sql
SHOW TABLES;
```

### 특정 테이블 보고싶을 때
```sql
SELECT * FROM `테이블명`;
```

- 테이블, 데이터베이스, 컬럼명 이름은 엇기호
- 문자는 단따옴표
- SQL는 소문자도 가능하지만 데이터와 쉽게 구분하기 위해 대문자 사용
- 엇기호 안써도 될 때가 있음
- 하지만 테이블명으로 create와 같은 예약어를 쓰고 싶은 경우 필요 
 
