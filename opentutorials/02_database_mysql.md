# 데이터베이스의 종류
- 관계형 데이터베이스
  - mysql ***
  - oracle
  - mssql
  - 이 셋은 sql이라는 데이터를 제어하기 위한 표준화된 문법을 공유함 (insert, select)
- nosql
  - 빅데이터를 다루는데는 관계형 데이터베이스는 한계가 있음
  - mongodb
  - 다양한 종류의 nosql 존재
    - http://nosql-database.org


## 데이터베이스 시스템의 구성 
- 이 전체를 데이터베이스라고 할 수 있음
- 웹서버 - 클라이언트와 유사
  - 웹서버가 제공
  - 웹클라이언트가 요청
    - 브라우저, 인터넷익스플로어, 파이어폭스
- 데이터베이스 서버
  - 데이터를 저장, 수정, 삭제, 정의
  - 서버 안에 데이터 베이스가 존재 - mov​ie, music
  - 데이터베이스: 테이블이라는 것을 카테고라이징 - album, favotie, musician
  - 필드: 행과 열을 통해서 접근 - 교차점 셀 하나 
  - 레코드: 구체적인 데이터를 의미 (행은 추상적인 개념)
- 데이터베이스 클라이언트
  - 서버에 요청해서 명령, 데이터 가져옴, 서버의 상태 확인 
  - navicat
    - 비쌈
  - mysql client
```
create database 000
drop database 000
show databases - 데이터 베이스 리스트 보여줌 
use music - music 데이터베이스 불러옴
show tables - 테이블의 리스트를 열람
select * from favorite_music - 테이블 열람 
즉, 클라이언트를 통해 명령어를 입력해서 서버를 제어 
```

즉,  
데이터베이스 서버 > 데이터베이스 > 테이블 > 행, 열 > 필드  
이 전체적인 것이 데이터베이스  
