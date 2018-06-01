# index (생활코딩)

## 색인
- 조회할 때 원하는 행을 빠르게 찾을 수 있게 준비해둔 데이터
- 데이터가 많은 경우 데이터를 찾는데 시간이 많이 걸릴 수 있음 
- 데이터베이스에서 매우 중요
 
## 인덱스의 종류 

- primary: 중복되지 않는 유일한 키
- normal: 중복을 허용하는 인덱스
- unique: 중복을 허용하지 않는 유일한 키
- foreign: 다른 테이블과의 관계쌍을 부여하는 키
- full text: 자연어 검색, myisam에서만 지원
- key를 지정하면, 그 키들을 통틀어서 인덱스라고 부름 
 
# 예제
```sql
DROP TABLE IF EXISTS `student`;
CREATE TABLE `student` (
  `id` tinyint(4) NOT NULL AUTO_INCREMENT,
  `name` char(4) NOT NULL,
  `address` varchar(50) NOT NULL,
  `department` enum('국문과','영문과','컴퓨터공학과','전자공학과','물리학과') NOT NULL,
  `introduction` text NOT NULL,
  `number` char(255) NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `idx_number` (`number`) USING BTREE,
  KEY `idx_department` (`department`),
  KEY `idx_department_name` (`department`,`address`),
  FULLTEXT KEY `idx_introduction` (`introduction`)
) ENGINE=MyISAM AUTO_INCREMENT=9 DEFAULT CHARSET=utf8;
INSERT INTO `student` VALUES (1, '이숙경', '청주', '컴퓨터공학과', '저는 컴퓨터 공학과에 다닙니다. computer', '0212031');
INSERT INTO `student` VALUES (2, '박재숙', '서울', '영문과', '저는 영문과에 다닙니다.', '0512321');
INSERT INTO `student` VALUES (3, '백태호', '경주', '컴퓨터공학과', '저는 컴퓨터 공학과에 다니고 경주에서 왔습니다.', '0913134');
INSERT INTO `student` VALUES (4, '김경훈', '제천', '국문과', '제천이 고향이고 국문과에 다닙니다.', '9813413');
INSERT INTO `student` VALUES (6, '김경진', '제주', '국문과', '이번에 국문과에 입학한 김경진이라고 합니다. 제주에서 왔어요.', '0534543');
INSERT INTO `student` VALUES (7, '박경호', '제주', '국문과', '박경호입니다. 잘 부탁드립니다.', '0134511');
INSERT INTO `student` VALUES (8, '김정인', '대전', '영문과', '김정인입니다. 대전에서 왔고, 영문과에 다닙니다.', '0034543');
```

# primary key

- 테이블 전체를 통틀어서 중복되지 않는 값을 지정해야 한다. 중복되면 에러 발생 
- where 문을 이용해서 데이터를 조회할 때 가장 고속으로 데이터를 가져올 수 있다.
- where 조건에 id를 기술하게 되면 빠르게 가져옴
- 테이블마다 딱 하나의 primary key를 가질 수 있다.

```sql
select * from student where id=3;
 ```
 
# unique key

- 테이블 전체를 통틀어서 중복되지 않는 값을 지정해야 한다. e.g.학번 - 학번은 사람마다 중복되지 않음 
- 'ind_number'가 unique key의 이름이 됨 
- 지정해주지 않으면 자동 지정 
- 고속으로 데이터를 가져올 수 있다.
- primary보다는 느릴 수 있음 
- 여러개의 unique key를 지정할 수 있다.
- primary와의 차이점 : primary는 한번만 정의 / unique는 여러번 정의 가능 

```sql
select * from student where number=0534543;
```

## normal key

- 중복을 허용한다. e.g. 전공처럼 여러명이 중복 가능 
- primary, unique 보다 속도가 느리다.
- normal key 안걸어 놓은 것보다는 빠름
- 여러개의 키를 지정할 수 있다.
 
 ```sql
select * from student where department='국문과'
```

## full text

- mysql의 기본설정(ft_min_word_len)이 4로 되어 있기 때문에 최소 4글자 이상을 입력하거나 이 값을 조정해야 한다.
- mysql은 전문 검색 엔진이 아니기 때문에 한글 검색이 잘 안된다.
- 형태소 분석이 연류되어있는 문제
- 전문검색엔진으로 lucene, sphinx 참고
- 모두 오픈소스, 좋은 성능
- 스토리지 엔진 중 myisam에서만 사용가능

```sql 
SELECT introduction FROM student WHERE MATCH (introduction) AGAINST('영문과에');
```

## 중복키

- 하나의 키에 여러개의 칼럼을 포함
- 인덱스의 한 형태가 아니라 인덱스를 만드는 스타일
- primary, normal, unique에서 두개 이상의 칼럼을 키로 지정 가능 

```sql
select * from student where department='국문과' AND address='제주';
```

## 인덱스의 정의 방법

- 많은 경우가 필요
- 자주 조회되는 칼럼에 적용
- 조회 시 오랜시간을 소모하는 컬럼에 적용
데이터가 긴 경우 인덱스를 사용하지 않는다.
e.g. url 
