---

title: "SQL: 데이터 분석 고급 SQL"
date: "2025-02-18"
thumbnail: "/assets/img/thumbnail/SQLlogo.png"
---

## 연재중

현재 해당 과정은 하나씩 여러가지의 답변을 기준으로 작성해나가는 중임.



## 섹션1

DML(Data Manipulation Language)

데이터 조작하는 언어로 

데이터에 변형을 가하는 종류다. (삽입, 수정, 삭제)

= SELECT, INSERT, UPDATE, DELETE



DDL와 다른점은 문구이 다르고,

DDL은 영구변화 DML은 임시 변경 후 뒤로 가기 가능 차이



#### 1-1)INSERT

`INSERT INTO (table name) VALUES (Value_list);`

컬럼의 순서대로 입력한다.



Table: Salary

| ID   | NAME | SALARY | DATE |
| ---- | ---- | ------ | ---- |

예시인데,



`INSERT INTO` Salary `Values`('1','A','250',2020-03-31')

하면 순서대로 값에 들어가는 것이다.



대신 지정해서 넣을수도 있다.



`INSERT INRO` Salary(Id, Salary) `VALUES` ('2','550')

이러면 2, Null, 550, Null로 들어간다. (디폴트 = Null)



#### 1-2)UPDATE

`UPDATE (table name) SET colunme = values`

이는 내용을 수정하는 것이다.



`UPDATE Salary SET Salary = Salry + 100;`

을 하면 기존의 Salary 테이블에 Salary값이 +100이 되어 수정된다.



즉 SET에서 =는 비교가 아닌 대입연산자다.



만약 특정 행만 넣고 싶다면?

`...Salary + 100 Where ID =2;`

WHERE 조건문을 통해서 ID 가 2인 행만 적용시킨다.

그러면 ID가 2인 행만 Salary값이 늘어난다.



#### 1-3) DELECT

`DELECT (DELETE FROM (table name) + WHERE (requirement)`

컬럼은 삭제하되 구조는 남은 상태라고 생각하면 된다.



기본적 형식은 UPDATE와 같음,



해당 관련하여



LeetCode 627. Swap Salary ,

LeetCode 196. Delete Duplicate Emails

를  풀것이다.



#### LeetCode 627. Swap Salary 

```
문제 : Salary Table에서 아래 Example과 같은 Table에서 M=Male F=Female 이다. m와 f값을 스왑해달라.
Temp를 쓰지말고 UPDATE statement를 써서 바꿔라.

NOT SELECT .
```

즉 그러면 UPDATE _ SET_ 문을 써야되니까.  

간단하게 입력을 해보자.

```sql
UPDATE "table"
SET "column" 
```

예시로 CASE _ WHEN _ THEN를 써서 하나씩 여러개 바꿀 수 있다.



```sql
UPDATE _
SET _ = case
		WHEN (조건) THEN (변할 예정 값) --조건이 True면 THEN 변경
        ..
        
        ELSE '_' --위 조건이 모두 아닌 경우의 출력
        END ; //끝내기
```



```sql
-- 답안A
UPDATE salary 
SET sex = CASE WHEN sex='f' THEN 'm'
            ELSE 'f' 
END;  
```

설명

UPDATE 테이블 SET 성이 F면 m으로 바꾸면 아니면 f로 변경

```sql
--답안B
UPDATE salary
SET sex = IF(sex = 'f', 'm', 'f');
```

설명

만약 성이 F면 M으로 아니면 F로 변경한다. 위랑 비슷한데 

여러가지 측면에서 A가 낫다고 생각이 든다.

(간단한 경우는 이거고 다중 조건이면 위가 더?)



#### LEET CODE 196. Delete Duplicate Emails

문제: 중복이 되는 이메일을 삭제하고 싶다. (Person Table)

하지만 최소한 한 개는 남겨야한다.(ID가 smallest인것만)



즉, John 중복을 날리는데 3번은 날려야하는 것



필요개념) 서브쿼리 = 쿼리 안에 쿼리를 통해서 조건부여



```sql
-- Email로 묶고 ID가 작은 경우를 출력하는 거다.
SELECT Email, MIN(Id)  
FROM Person 
GROUP BY Email
```

즉 그러면 우리가 했던 값들이 보관해야되는 것이 되는 것이다 = 서브쿼리



```sql
SELECT sub.min_id
FROM (
SELECT Email, Min(Id) AS min_id
FROM Person
Group By Email)
sub
```

실행하면 오류가 걸림

why? 동작하지 못하게 세팅이 되어있어서 짤라야된다고 함

```sql
-- 정답
DELECT
FROM Person
WHERE ID Not in (
SELECT sub.min_id
FROM(
SELECT Email, Main(Id) AS min_id
FROM Person
Group By Email) sub)
```

ID컬럼을 기준으로

서브쿼리 제외하고 나머지를 DELECT하는 구문을 생성

NOT IN을 통해서 (...)안에 있는 것을 제외한 나머지를 삭제 시키는 것이다.



```sql
-- 여러가지 연습 Row_number
DELETE FROM Person
WHERE id IN (
    SELECT id
    FROM (
        SELECT id,
               ROW_NUMBER() OVER (PARTITION BY email ORDER BY id) as id_rank
        FROM Person
    ) ranked_emails
    WHERE id_rank > 1
);
-- Row_number
```

1. 내부쿼리의 동작

Row_number로 사용했다.

윈도우 함수 Row_number는 순위시스템이다.



ROW_NUMBER () OVER (PARTITON BY '그룹화' ORDER BY '순위기준점')

`(PARTITION BY email ORDER BY id)` 이니까

이메일로 그룹을 짜주고 ID를 순위로 매긴다. 그러면 ID가 작으면 1순위.



2. 외부쿼리의 동작

```sql
SELECT id
FROM ( ... ) ranked_emails  -- 내부 서브쿼리
WHERE id_rank > 1
```

id_rank가 1순위가 아닌 것을 뽑는다. (즉 1제외 중복된 것 거름망)



3. DELECT동작

```sql
DELECT 
WHERE id IN ( 외부 서브 쿼리)
```

로 외부 서브 쿼리에 해당하는 것들을 제거해준다.



```sql
-- 여러가지 문제연습 CTE
-- Row_number는 CTE로 바꿀 수 있다.

-- CTE?: Common Table Expressions = 임시 데이터 세트
-- 위에서 쿼리를 단계별로 정리했으니

/*
=> CTE변경
WITH CTE AS (
내부서브쿼리
)

DELECT 
WHERE id IN ( 외부 서브 쿼리)
*/
```

```sql
WITH CTE_practice AS (
    SELECT id,
           ROW_NUMBER() OVER (PARTITION BY email ORDER BY id) as id_rank
    		-- 서브쿼리
    FROM Person
)

DELETE FROM Person -- DELECT 문
WHERE id IN (SELECT id FROM CTE_practice WHERE id_rank > 1); -- 외부쿼리
```

로 나타냈는데 실무적으로 무엇이 좋은 코드(?)인가에 대해서 질문을 남겼으니 추후 확인예정이다.