---
title: Mysql 코딩테스트 문법 정리1
date: 2023-01-21 23:58:25
tags:
  - Coding test
  - SQL
categories:
  - Coding test
  - SQL
---

## 기본 문법

### ORDER BY

- ASC: 오름차순
- DESC: 내림차순

## 문자열 자르기

### SUBSTRING

- SUBSTRING(문자열, 시작 위치, 시작 위치부터 가져올 문자수)

```SQL
SELECT SUBSTRING('123456789', 7);
>> 789
SELECT SUBSTRING('123456789', 3, 5);
>> 34567
```

### SUBSTRING_INDEX

- SUBSTRING_INDEX(문자열, 구분자, 구분자 Index)

```SQL
SELECT SUBSTRING_INDEX('사과,바나나,딸기,포도', ',', 3);
>> 사과,바나나,딸기
SELECT SUBSTRING_INDEX('사과,바나나,딸기,포도', ',', -3);
>> 바나나,딸기,포도
```

- SELECT SUBSTRING_INDEX(SUBSTRING_INDEX(문자열, 구분자, 구분자 Index), 구분자, -1)

```SQL
SELECT SUBSTRING_INDEX(SUBSTRING_INDEX('사과,바나나,딸기,포도', ',', 2), ',', -1)
>> 바나나
```

### CONCAT

```SQL
>> 01012345678
CONCAT(SUBSTRING(TLNO, 1, 3), '-', SUBSTRING(TLNO, 4, 4), '-', SUBSTRING(TLNO, 8)) AS '전화번호'
>> 010-1234-5678
```

## 시간 관련 함수

### DATE_FORMAT

- DATE_FORMAT(날짜 , 형식)

```SQL
SELECT DATE_FORMAT(NOW(),'%Y-%m-%d') AS DATE FROM DUAL
>>2022-01-21
```

#### DATE_FORMAT 형식

| 형식 |           설명           |
| :--: | :----------------------: |
|  %Y  |        4자리 년도        |
|  %y  |        2자리 년도        |
|  %M  |       긴 월(영문)        |
|  %b  |      짧은 월(영문)       |
|  %W  |    긴 요일 이름(영문)    |
|  %a  |   짧은 요일 이름(영문)   |
|  %i  |            분            |
|  %T  |         hh:mm:SS         |
|  %m  |     숫자 월(두자리)      |
|  %c  | 숫자 월(한자리는 한자리) |
|  %d  |       일자(두자리)       |
|  %e  |  일자(한자리는 한자리)   |
|  %l  |       시간(12시간)       |
|  %H  |       시간(24시간)       |
|  %r  |      hh:mm:ss AM,PM      |
|  %S  |            초            |

### YEAR, MONTH, DAY

- YEAR(DATE_VALUE)
- MONTH(DATE_VALUE)
- DAY(DATE_VALUE)

#### 날짜 관련 함수 참고 자료

- https://jang8584.tistory.com/7

### DATE_ADD, DATE_SUB

```SQL
SELECT DATE_ADD(NOW(), INTERVAL 1 SECOND);
SELECT DATE_ADD(NOW(), INTERVAL 1 MINUTE);
SELECT DATE_ADD(NOW(), INTERVAL 1 HOUR);
SELECT DATE_ADD(NOW(), INTERVAL 1 HOUR);
SELECT DATE_ADD(NOW(), INTERVAL 1 MONTH);
SELECT DATE_ADD(NOW(), INTERVAL 1 YEAR);
SELECT DATE_ADD(NOW(), INTERVAL -1 YEAR);

SELECT DATE_SUB(NOW(), INTERVAL 1 SECOND);
```

### DATEDIFF, TIMESTAMPDIFF

- 날짜 차이 계산

```sql
SELECT DATEDIFF('2020-05-27 15:00:00','2020-05-20 13:00:00') AS DATEDIFF;
# 결과 : 7
```

- 시간 차이 계산
- 시간 표현 단위는 second, minute, hour, day, week, month, year 등이 있음

```sql
SELECT TIMESTAMPDIFF(MINUTE, '2020-05-20 13:00:00','2020-05-20 17:00:00') AS TIMESTAMPDIFF;
# 결과 : 240
```

## 반올림, 올림, 버림

- ROUND(값, 자릿수): 해당 자리수까지 반올림
- CEIL(값): 올림
- FLOOR(값): 소수 버림
- TRUNCATE(값, 자리수): 해당 자리수까지 버림

```SQL
SELECT ROUND(0.512) AS '반올림'
    ,ROUND(0.567, 2) AS '반올림 자릿수 설정'
    ,CEIL(0.1) AS '올림'
    ,FLOOR(0.911) AS '소수 모두 버림'
    ,TRUNCATE(0.21, 1) AS '소수 자리수까지 버림'

>>1, 0.57, 1, 0, 0.2
```

## 조건문

```SQL
CASE
    WHEN 조건1 THEN '조건1 반환값'
    WHEN 조건2 THEN '조건2 반환값'
    ELSE '충족되는 조건 없을때 반환값'
END AS '정할 칼럼명'
```

## UNION

- 대응하는 칼럼의 이름이 다르다면 통일한다.
- 단, 별칭은 UNION을 사용하기 전에 선언해야 한다.

```SQL
SELECT asia AS 'country' FROM TABLE_1
UNION -- UNION DISTINCT과 결괏값이 같다
SELECT country FROM TABLE_2;
```

## LIMIT

- 상위 데이터 1개

```SQL
SELECT name from animal_ins order by datetime asc limit 1;
```

- 두 번째 데이터부터 10개

```SQL
SELECT name from animal_ins order by datetime asc limit 1,10;
```

- 11번째 데이터부터 10개

```SQL
SELECT name from animal_ins order by datetime asc limit 10, 10;
```

## 사이값 가져오기

```SQL
SELECT * FROM contacts WHERE contact_id BETWEEN 10 AND 20;  # 동일하다
SELECT * FROM contacts WHERE contact_id >= 10 AND contact_id <= 20; # 동일하다
```

## 형변환

```SQL
CAST(컬럼명, 값 AS 변경하려는 TYPE명)

SELECT CAST("2021-09-27" AS DATE);
```

|    형식    |                                 설명                                  |
| :--------: | :-------------------------------------------------------------------: |
|   BINARY   |                          값을 binary로 변환                           |
|    CHAR    |                          값을 문자열로 변환                           |
|    DATE    |                     값을 yyyy-mm-dd의 date로 변환                     |
|  DATETIME  |             값을 yyy-mm-dd hh:mm:ss 의 datetime으로 변환              |
|    TIME    |                     값을 hh:mm:ss의 time으로 변환                     |
|  DECIMAL   | 값을 최대자릿수인(M), 소수점 이하 자릿수(D)로 지정하여 decimal로 변환 |
|   NCHAR    | 값을 nchar로 변환(char랑 비슷하지만, 국가별 문자 세트로 문자열 생성)  |
|  SIGNED ~  |           값을 signed(부호 있는 64비트 정수)로 변환합니다.            |
| UNSIGNED ~ |           값을 signed(부호 없는 64비트 정수)로 변환합니다.            |

## 임시테이블 생성

```SQL
WITH RECURSIVE CTE AS (
    SELECT 0 AS RNUM
    UNION ALL
    SELECT RNUM + 1 FROM CTE
    WHERE RNUM < 23
)
# SELECT RNUM FROM CTE
```

## INNER JOIN

```sql
select *
from A inner join B
on A.id = B.id;
```

## OUTER JOIN

```
select *
from A left outer join B
on A.id = B.id;
```

```
select *
from A right outer join B
on A.id = B.id;
```

### FULL OUTER JOIN

- Mysql에서는 full outer join을 기본적으로 제공하지 않는다.

```SQL
select *
from A right outer join B
on A.id = B.id;
UNION
select *
from A right outer join B
on A.id = B.id;
```

## coalesce

- NULL이 아닌 첫번째 값을 반환한다.
- coalesce(A, B)
