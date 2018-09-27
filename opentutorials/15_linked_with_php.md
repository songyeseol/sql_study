# 프로그래밍과 데이터베이스의 관계

- 프로그래밍과 데이터베이스는 무관
- 데이터베이스는 독립적인 시스템으로 프로그래밍과 상관없이 사용 가능
- 데이터베이스를 이해하고 있다면 여기에 프로그래밍을 결합해서 많은 것을 할 수 있음
 
### API

- Application Programming Interface
- 데이터베이스는 API를 제공한다
- PHP와 같은 프로그래밍 언어들은 이 API를 이용해서 데이터베이스를 이용
 
### PHP와 MYSQL

- 가장 많이 사용되는 조합 
- php는 웹에 특화되어있는 언어
- php는 다양한 데이터베이스 시스템과 연동될 수 있음
- mysql도 다양한 언어와 연동될 수 있음 
 
### 데이터베이스의 내용을 웹으로 출력하기

#### STEP1) 데이터 입력 


```sql
CREATE DATABASE `class` CHARACTER SET utf8 COLLATE utf8_general_ci;
USE class;
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

- apm setup monitor에서 mysql 관리 클릭
- 로그인
- sql에 데이터 입력

#### STEP2) 웹페이지 만들기 

```
<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html;charset=utf-8" >
    <style>
        table{border:1px solid gray; border-collapse:collapse;}
        td{border:1px solid gray;padding:5px;}
    </style>
</head>
<body>
<?php
$conn = mysql_connect("localhost", "root", "1234");
mysql_query('SET NAMES utf8');
if (!$conn) {
    echo "Unable to connect to DB: " . mysql_error();
    exit;
}
if (!mysql_select_db("class")) {
    echo "Unable to select mydbname: " . mysql_error();
    exit;
}
$sql = "SELECT *
        FROM  student
    LIMIT 10";
$result = mysql_query($sql);
if (!$result) {
    echo "Could not successfully run query ($sql) from DB: " . mysql_error();
    exit;
}
if (mysql_num_rows($result) == 0) {
    echo "No rows found, nothing to print so am exiting";
    exit;
}
// While a row of data exists, put that row in $row as an associative array
// Note: If you're expecting just one row, no need to use a loop
// Note: If you put extract($row); inside the following loop, you'll
//       then create $userid, $fullname, and $userstatus
echo "<table>";
while ($row = mysql_fetch_assoc($result)) {
    echo "<tr><td>{$row['id']}</td><td>{$row['name']}</td><td>{$row['department']}</td></tr>";
}
echo "</table>";
mysql_free_result($result);
?>
</body>
</html>
```

- 하이라이트 부분 자기 비밀번호로 바꾸기
- 메모장에 붙여넣고 'list.php' 제목으로 저장
- 인코딩은 utf-8
l- ocalhost/list.php로 접속 
