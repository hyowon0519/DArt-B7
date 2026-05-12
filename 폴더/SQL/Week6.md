# SQL_BASIC 6주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_6th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**6주차 과제는 강의 내용을 정리하는 것과 함께, 프로그래머스에서 제공하는 SQL 문제를 직접 풀어보는 실습도 병행합니다.** 강의에서는 **배운 내용을 정리하고 주요 쿼리 예제를 정리**하며, 프로그래머스 문제는 **직접 풀어본 뒤 풀이 과정과 결과, 배운 점을 함께 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_6th

### 섹션 6. 다량의 자료를 연결 : JOIN 

### 5-1. Intro

### 5-2. JOIN 이해하기

### 5-3. 다양한 JOIN 방법

### 5-4. JOIN 쿼리 작성하기 

### 5-5. JOIN을 처음 공부할 때 헷갈렸던 부분

### 5-6. JOIN 연습문제 1~2번

### 5-6. JOIN 연습문제 3~5번

### 5-7. 정리



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | ✅         |
| 6주차 | 섹션 **5-1** ~ **5-7** | ✅         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<!-- 여기까진 그대로 둬 주세요-->

<br>

---

# 1️⃣ 개념정리

## 5-2. JOIN 이해하기


✅ 학습 목표 :
* JOIN에 대한 정의와 필요성에 대해 설명할 수 있다.


### JOIN이란?
- 서로 다른 데이터 테이블을 연결하는 것
- 공통으로 존재하는 컬럼(Key)이 있다면 JOIN 가능
- 보통 id 값을 많이 사용하며, 날짜(Date) 기준으로도 JOIN 가능

### JOIN을 사용하는 이유
- 관계형 데이터베이스(RDBMS)는 정규화를 통해 데이터를 여러 테이블로 나누어 저장함
- 예: User Table에는 유저 정보만, Order Table에는 주문 정보만 저장
필요한 데이터를 사용할 때 JOIN으로 연결해서 활용

### 핵심 정리
- JOIN이 어려운 이유는 문법보다 테이블 구조가 익숙하지 않기 때문
- 문제를 많이 풀어보며 JOIN 흐름을 익히는 것이 중요함



## 5-3. 다양한 JOIN 방법


✅ 학습 목표 :
* JOIN 방법들의 종류를 설명할 수 있다. 
* 각 JOIN 방법들의 차이점에 대해서 설명할 수 있다. 

INNER JOIN:	두 테이블의 공통 데이터만 연결
LEFT JOIN:	왼쪽 테이블 기준으로 연결
RIGHT JOIN:	오른쪽 테이블 기준으로 연결
FULL OUTER JOIN:	양쪽 데이터를 모두 연결
CROSS JOIN:	두 테이블의 모든 경우의 수를 연결

*추가 정리*
- 처음에는 LEFT JOIN 위주로 연습해도 충분함
- CROSS JOIN은 데이터 양이 크게 증가할 수 있어 주의 필요


## 5-4. JOIN 쿼리 작성하기 

✅ 학습 목표 :
* JOIN을 사용한 문법에 대해 이해하여 적용할 수 있다.
* JOIN 을 활용한 쿼리를 작성할 수 있다. 


### JOIN 쿼리 작성 순서
JOIN 쿼리 작성 순서
사용할 테이블 확인
기준 테이블 정하기
JOIN Key 찾기
결과 예상하기
쿼리 작성 및 검증하기

[기본 문법]
SELECT
  A.col1,
  B.col2
FROM table1 AS A
LEFT JOIN table2 AS B
ON A.key = B.key

[예시]
SELECT
  tp.*,
  p.kor_name
FROM basic.trainer_pokemon AS tp
LEFT JOIN basic.pokemon AS p
ON tp.pokemon_id = p.id

[핵심 포인트]
- ON 뒤에는 공통 Key 작성
- 테이블 이름이 길면 AS로 별칭(Alias) 사용 가능
- JOIN은 여러 번 연속해서 사용할 수 있음


## 5-6. JOIN 연습문제 1~5번 


✅ 학습 목표 :
* 연습문제(3문제 이상) 푼 것들 정리하기


[1번: 트레이너가 보유한 포켓몬 수 계산하기]

SELECT
  p.kor_name,
  COUNT(tp.id) AS pokemon_cnt
FROM (
  SELECT *
  FROM basic.trainer_pokemon
  WHERE status IN ("Active", "Training")
) AS tp
LEFT JOIN basic.pokemon AS p
ON tp.pokemon_id = p.id
GROUP BY p.kor_name
ORDER BY pokemon_cnt DESC

- 먼저 WHERE로 데이터를 줄인 후 JOIN하는 것이 효율적임

[3번: 고향에서 포켓몬을 잡은 트레이너 수 계산하기]

SELECT
  COUNT(DISTINCT tp.trainer_id) AS trainer_uniq
FROM basic.trainer AS t
LEFT JOIN basic.trainer_pokemon AS tp
ON t.id = tp.trainer_id
WHERE
  tp.location IS NOT NULL
  AND t.hometown = tp.location

- DISTINCT를 사용해 중복 트레이너 제거
- JOIN 시 데이터 행 수가 늘어날 수 있다는 점 주의


[5번:Incheon 출신 트레이너의 세대별 포켓몬 수 계산하기]
SELECT
  p.generation,
  COUNT(tp.id) AS pokemon_cnt
FROM basic.trainer_pokemon AS tp
LEFT JOIN basic.trainer AS t
ON tp.trainer_id = t.id
LEFT JOIN basic.pokemon AS p
ON tp.pokemon_id = p.id
WHERE
  t.hometown = "Incheon"
  AND tp.status IN ("Active", "Training")
GROUP BY p.generation

- 여러 개의 JOIN을 연속으로 사용할 수 있음
- 기준 테이블을 잘 정하는 것이 중요함




<br>

<br>

---

# 2️⃣ 확인문제 & 문제 인증

## 프로그래머스 문제 

https://school.programmers.co.kr/learn/courses/30/lessons/131533

> 상품 별 오프라인 매출 구하기

https://school.programmers.co.kr/learn/courses/30/lessons/133027

> 주문량이 많은 아이스크림들 조회하기

<!-- 정답을 맞추게 되면, 정답입니다. 이 부분을 캡처해서 이 주석을 지우시고 첨부해주시면 됩니다. --> 



---

# 3️⃣ 참고자료

JOIN 에 대해서 그림으로 쉽게 이해할 수 있는 자료들도 있어서 첨부합니다. 아래의 블로그도 학습할 때 같이 참고해주세요.

1. https://data-marketing-bk.tistory.com/entry/SQL-JOIN-%ED%95%9C-%EB%B0%A9%EC%97%90-%EC%A0%95%EB%A6%AC-%EA%B0%9C%EB%85%90%EB%B6%80%ED%84%B0-%EC%BD%94%EB%93%9C%EA%B9%8C%EC%A7%80-%EC%9D%B4%EA%B2%83%EB%A7%8C-%EB%B3%B4%EC%9E%90



2. https://velog.io/@wijoonwu/JOIN

<br>

### 🎉 수고하셨습니다.
