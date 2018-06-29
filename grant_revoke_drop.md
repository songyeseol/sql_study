 
# Grant

사용자에 따라서 접근할 수 있는 데이터와 사용할 수 있는 기능을 제한
사용자를 생성하고, 권한을 부여함 
 
## 문법

```sql
GRANT 권한 ON 데이터베이스.테이블 TO '아이디'@'호스트' IDENTIFIED BY '비밀번호';
```

### 권한의 제한 
- 사용할 수 있는 권한을 제한 
- 권한 템플릿
  - 운영하는 사람의 role에 따라서 부여하게 되는 권한들이 달라짐
  - 불필요하게 더 많은 권한을 줘서 리스크를 만드는 것을 방지

### 대상의 제한
- 데이터베이스.테이블
- class.student
  - class라는 데이터베이스 안에 속해있는 student 테이블에 대해서만 권한을 줌 
- class.* 
  - class안의 모든 테이블에 대한 권한 
- 사용자가 제어할 대상이 되는 데이터베이스, 테이블을 지정
- *을 사용하면 모든 데이터베이스, 테이블을 제어 대상으로 함

### 사용자의 제한
- '아이디'@'호스트' IDENTIFIED BY '비밀번호'
- 데이터베이스 서버에 접속하는 사용자를 제한
- 호스트는 접속자가 사용하는 머신의 IP를 의미
- 특정하지 않다면 %를 사용
- egoing@123.100.100.100 : IP 123.100.100.100인 머신에서 접속한 ID egoing
- egoing@% : IP 관계없이 ID가 egoing인 사용자

## 예제
```sql
GRANT DELETE,INSERT,SELECT,UPDATE ON class.* TO `dev`@`%` IDENTIFIED BY '1234';
```

- ID가 dev, 비밀번호가 1234인 사용자가 class 데이터베이스만 접근하게 하려면 아래와 같이 한다.
- 어떠한 IP로 접근을 하든 허용

```sql
GRANT ALTER, CREATE, DELETE, DROP, INDEX, INSERT, SELECT, UPDATE ON *.* TO `archi`@`100.100.100.100` IDENTIFIED BY '1234';
```

- ID가 archi, 비밀번호가 1234이고 클라이언트의 IP가 100.100.100.100인 사용자가 모든 데이터베이스에 접근하면서 설계자의 권한 템플릿을 이용할 때
 
```sql
SHOW GRANTS [FOR 사용자];
```
- [for 사용자] 안쓰면 내 권한 볼 수 있음

# REVOKE

사용자의 권한을 제거

## 문법

```sql
REVOKE 권한 ON 데이터베이스.테이블 FROM 사용자
```

## 예제

'''sql
revoke DELETE on class.* from dev;
```
사용자 dev의 데이터베이스 class의 DELETE 권한을 제거 


# DROP USER
사용자를 삭제 

## 문법 

```sql
DROP USER user [, user] ...;
```
복수의 유저 삭제하고 싶을 때 comma

## 예제
```sql 
DROP USER `dev`@`%`;
```


## 권한 테이블
[생활코딩 참고](https://opentutorials.org/course/195/1406)
