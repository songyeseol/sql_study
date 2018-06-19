# INSERT 

## 문법

```sql
INSERT INTO table_name VALUES (value1, value2, value3,...)
INSERT INTO table_name (column1, column2, column3,...) VALUES (value1, value2, value3,...)
```

- 컬럼 순서와 정확하게 일치해야 함

## 예제

```sql
INSERT INTO `student` VALUES ('2', 'leezche', '여자', '서울', '2000-10-26');
INSERT INTO `student` (`id`, `name`, `sex`, `address`, `birthday`) VALUES ('1', 'egoing', '남자', 'seoul', '2000-11-16');
```
- 굳이 컬럼 이름 입력? >> 순서를 바꿔서 넣을 수 있음

### 기술하지 않아도 되는/기술하면 안되는 데이터가 있을 경우

```sql
INSERT INTO `student` (`id`, `name`, `sex`, `address`) VALUES ('3', 'egoing', '남자', 'seoul');
```
- birthday 삽입 안함 
- 0000-00-00 으로 나옴 
- 데이터베이스의 구조는 언제든지 변경될 수 있기 때문에 이 방식이 더 바람직
