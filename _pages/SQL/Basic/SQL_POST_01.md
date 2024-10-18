---
title: "SQL: 데이터 분석 기초 SQL"
date: "2024-10-17"
thumbnail: "/assets/img/thumbnail/SQLlogo.png"

---

## 수료

![SQL_01_over](../../../images/SQL_POST_01/SQL_01_over.jpg)

기초 수강을 하였는데 생각보다 재미있었다! 

이 글을 정리를 위해서 시작하고자 한다.



인프런에서 [백문이불여일타] 데이터 분석을 위한 기초 SQL 추천한다.



## 내용 정리

DQL (Data Query Language - 질의어)

```
select

데이터 조회시 사용
```



 

DML (Data Manipulation Language - 조작어)

```
Insert, Update, Delete..

데이터 조작할 때 사용
```



1. 해당강의는 데이터를 가져오는 것 위주의 강의이다.
2. 데이터를 가져와야지 분석을 하기 때문에 끌어올 수 있어야한다.
3. 데이터를 수정하고 지우는 것은 엔지니어의 영역



이후 강의는

- 이론을 바탕으로 문제풀이
- 해커랭크 코딩테스트를 병행한다.



= 이 강의는 데이터를 불러오는 것과 이론 설명 후 코딩테스트의 형식을 통해 이론과 실습을 진행함.



## 초급시작

데이터는 테이블형태로 지정된다

| 종류 | 이름 | 가격 |
| ---- | ---- | ---- |
| 과일 | 배   | 1200 |
| 채소 | 당근 | 800  |

우리가 잘 아는 엑셀과 같다고 생각하자.



가로 줄의 최상단으로 뻗어져나감 

=>  `종류, 이름, 가격`은 컬럼(colmn) 행



세로 줄로 아래로 뻗어져나감

=> `종류, 과일, 채소`는 로우(low)행



+) 잘모르겠으면 로우는 밑으로 가니까 컬럼은 가로겠네~ 하면 된다

(예전에 학교에서 배웠을 떄 이렇게 외웠다는..ㅋㅋ)



```sql
SELECT *
FROM Customers
```

이 구절을 보면 되는데

SELECT *을 통해 전체지정을 해준 후  FROM으로 내가 보고싶은 테이블 적기이다.



두개를 보고싶으면 `FROM apple, banana` 하면된다.



> 주의할점
>
> 전체지정을 하여 찾기를 하면 시간이 오래 걸린다. 그래서 상한을 걸어준다
>
> `LIMIT n`이다.



### 문제풀이

인터프리터를 MSSQL로 놓고 시작한다.

```
Select All 문제: 
Query all columns (attributes) for every row in the CITY table 

CITY테이블에 모든 컬럼과 모든 로우를 추출
```



```SQL
SELECT * -- 컬럼명이 붙는다 (제일 큰 분류)
FROM CITY -- 테이블명이 붙는다. (시트의 개념)
```



```
Weather Observation Station 1 문제:
Query a list of CITY and STATE from the STATION table.

City과 State를 가져와야된다. 어디서? STATION 테이블에서
```



```sql
SELECT CITY, STATE -- 컬럼인 city state
FROM STATION -- 테이블인 STATION 
```



## 연산과 조건절

실제로 모든 데이터를 볼일은 자주없고 특정성이 들어가 있는 작업들을 많이 보게 될 것이다.

이것이 Where(조건)이다.



```sql
WHERE Country = 'Germany'
WHERE Customer ID <50 .. Customer <>20..
AND Country='Germany'
```

대입연산과 비교연산자를 통해서 조건을 넣어줄 수 있다.

그리고 조건결합인 논리연산자(AND OR)처럼 추가 도킹이 가능하다.



### LIKE, IN, BETWEEN, IS NULL

LIKE = 문자열에서 패턴을 찾는다.

```sql
LIKE '%r' --앞에 무엇이 있든 상관없는 r
LIKE 'r%' --뒤에 무엇이 있든 상관없는 r
```



IN = 추가조건을 묶어준다

```sql
WHERE Country  IN ('Germany', 'France')
= WHERE Country = 'Germany' OR Country='France'
```

두 개는 같으나 가독성과 구문의 차이만 봐도 위가 Goat임을 알 수 있다.

IN은 마치 SUM(A, B, C..)다



BETWEEN = 조건 A와 B사이 출력한다. (부분조건)

```sql
BETWEEN 3 AND 5
= Where A >= 3 AND A <=5
```

3과 5를 포함하고 그 사이 값을 출력하라

즉 BETWEEN은 이상과 이하의 개념



IS NULL = NULL값 탐색

```sql
-- IS NULL (NULL값 찾기)
WHERE A IUNULL;
```

NULL은 배운 것처럼 하나의 공백이다.

NULL = Nam = Not a Number이다.



### LIKE의 심화과정

위 LIKE에서 `%r`이 있었다, 여기서 %를 '와일드카드' 라고 부른다.

어떤 것이 와도 상관없다 = Wild Card



```sql
WHERE Country LIKE 'Brazil'
= WHERE Country = 'Brazil'
```

둘은 같으나 단순하게 하나의 완전한 값을 찾는 위 상황이라면

LIKE보다는 = 가 더 처리가 빠르다.



언더바도 추가시킬 수 있다.

```sql
LIKE 'b%' -- B로 시작하는 단어 찾기
LIKE 'b_____' -- _5개로 b이후 5개만 찾기
```

%는 모두찾기 _는 갯수 지정 찾기다.



```sql
WHERE discount LIKE '50%' -- 이러면 %가 문제가 생기는데
WHERE discount LIKE '50\%' --이렇게 해주면 된다. \를 통해서 풀어준다고 보면 됨.
```



회사마다 사용하는 SQL이 다른데

`PostgreSQL, MSSQL, RedShift SQL`등 다양한 DB가 있다.

구글에 검색해서 찾는데 그때는 보통 `Redshift like % escape`으로 타이핑하면 좋다



### WHERE절 요약

BETWEEN은 범위검색형이고 AND와 친구다.

```sql
WHERE BETWEEN A AND B;
WHERE A > = B AND <= C;
```



IN = 값 목록의 지정 (SUM) + OR로 풀어쓰기 가능

```sql
WHERE [ ] IN (A,B, C...)	
```



IS NULL / IS NOT NULL 

```sql
WHERE [ ] IS (NOT) NULL
```



### 문제풀이

```
1. Revising the Select Query II
문제: Query the NAME field for all American cities in the CITY table with populations larger than 120000. 
The CountryCode for America is USA.

조건
1. 12만보다 큰 Code
2. Country Code가 USA
3. 큰 테이블은 CITY 컬럼은 NAME
```

```sql
SELECT name
FROM city
WHERE population > 120000
AND countrycode = 'USA'
```



```
2. Select By ID
문제 : Query all columns for a city in CITY with the ID 1661.

조건
1.모든 컬럼
2.ID는 1661
```

```sql
SELECT *
FROM citry
WHERE ID = 1661 --숫자니까 ''안들어감
```



``` 
3. Weather Observation Station 6
문제: Query a list of CITY names from STATION for cities that have an even ID number. 
Print the results in any order, but exclude duplicates from the answer.

조건
1. 테이블 City name 영어모음 시작 City 고르기
2. 중복제거 DISTINCT 넣기
3. 추가 답변으로 IN써보기
```

```sql
[1번 정답]
SELECT DISTINCT city 
FROM station
WHERE city LIKE 'a%'
OR city LIKE 'e%'
OR city LIKE 'o%'
OR city LIKE 'i%'
OR city LIKE 'u%'

[2번 정답]
SELECT DISTINCT CITY
FROM STATION
WHERE LEFT(CITY, 1) IN ('A', 'E', 'I', 'O', 'U')
```

나중을 생각하면 2번을 통해서 하면 가독성이 좋을 것 같아서 2번이 좋을듯 하다..!



```
4. Weather Observation Station 12
문제: Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.

조건
1. 모음 aeiou 시작은 x 끝나지도 x
2. 중복을 제거 (DISTINCT)
```

```sql
[1번정답]
SELECT DISTINCT city
FROM station
WHERE city NOT LIKE 'a%'
AND city NOT LIKE 'e%'
AND city NOT LIKE 'i%'
AND city NOT LIKE 'o%'
AND city NOT LIKE 'u%' --동시니까 AND
AND city NOT LIKE '%a'
AND city NOT LIKE '%e'
AND city NOT LIKE '%i'
AND city NOT LIKE '%o'
AND city NOT LIKE '%u'


[2번정답]
SELECT DISTINCT CITY
FROM station
WHERE lEFT(city,1) NOT IN ('a', 'i', 'e', 'o', 'u')
AND RIGHT(city,1) NOT IN ('a', 'i', 'e', 'o', 'u')
```

이것도 가독성을 생각해서 후자가 더 편리할 것 같다.



이런 의문이 든다. IN과 LIKE는 서로 어떨 때 쓰는게 유용한가?



성능, 가독성부분은 LIKE보다 IN이 좋다고 한다.

즉. 단순히 앞글자 뒷글자 확인후 IN의 체크가 더 좋고 가독성도 IN이 높힐 수 있다. (리스트형식)



구체적인 요구사항은 LIKE가 더좋다고한다.

LIKE는 문자열 패턴 매칭에 강점이 있기에 복잡한 매칭일떄 쓴다.

`LIKE %pattere%`같이 특정패턴의 포함일때!





## ORDER BY 정리

정렬하기 = ORDER BY 



```sql
SELECT *
FROM Customers
WHERE -
ORDER BY customerid DESC --(내림차순)
ORDER BY Customerid ASC --(오름차순) - Default
```

```sql
--응용하면?
ORDER BY Price DESC --특정 테이블 가격의 내림차순

--조건으로 상단에 추가
WHERE price >=20
ORDER BY 
```



### 문제풀기

```
1.Employee Names
문제: Write a query that prints a list of employee names (i.e.: the name attribute) 
from the Employee table in alphabetical order.

조건
1. list of employee names
2. ASC (aplhabetical order)
3. Talbe : employee
```

```sql
SELECT name
FROM employee
ORDER BY name ASC
```



```
2.Employee Salaries
문제: Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than  per month who have been employees for less than  months. 
Sort your result by ascending employee_id.

조건
1.월 2000$ 이상
2.근무 10달 미만
3.ID정렬
```

```sql
SELECT name 
FROM employee
WHERE salary > 2000 
AND months < 10 
ORDER BY employee_id  
```



### 간단함수 설명 및 문제풀이

```
LEFT = 왼 , RIGHT = 오
SUBSTRING = 시작위치~ n까지
= SUBSTR (약자)

ORDER BY RIGHT (name,3), id
조건절의 두번째는 뒤로 
```

여기서 생각한게 ORDER BY에 _ 표현이 들어갈 수 있을까?

=> NO였다. ORDER BY는 컬럼이나 표현식 정렬이기에 와일드카드는 불가능 (NOT 문자열)



```
1. Weather Observation Station 15
문제: Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in STATION that is less than 137.2345. Round your answer to 4 decimal places.

조건
1.쿼리 LONG_W 부르기
2.LAT_N보다 큰것
3. STATION 테이블
4. ROUND함수 사용
5. Less than 137.2345보다 작은
6. 소수점 n자리 SELECT
7. 최대한개만 출력 
```

```sql
SELECT ROUND (LONG_W,4)
FROM station
WHERE LAT_N < 137.2345
ORDER BY LAN_T_N DESC
```



끝.