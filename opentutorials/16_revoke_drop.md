 

# REVOKE

사용자의 권한을 제거

## 문법

```sql
REVOKE 권한 ON 데이터베이스.테이블 FROM 사용자
```

## 예제

```sql
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
