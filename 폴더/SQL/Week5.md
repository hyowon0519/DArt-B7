# SQL_BASIC 5주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_5th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**5주차 과제는 문제 풀이를 중심으로**, 강의에서 제시된 예제 문제 중 **3 문제 이상을 선택하여 직접 풀어본 뒤**, 강의 영상의 풀이와 비교해 **틀린 부분, 맞은 부분, 새롭게 배운 개념**을 구체적으로 정리해주세요. (적어도 4문제는 정리해야 합니다.) 완성된 과제는 Gihub에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀(수행 인증샷은 필수입니다.)** 



## SQL_BASIC_5th

### 섹션 5. 데이터 탐색 - 변환

### 4-4. 날짜 및 시간 데이터 이해하기(2) (EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME)

### 4-5. 시간 데이터 연습문제 1~2번

### 4-5. 시간 데이터 연습문제 3~5번

### 4-6. 조건문 (CASE WHEN, IF)

### 4-7. 조건문 연습 문제

### 4-8. 정리

### 4-9. BigQuery 공식 문서 확인하는 법

(강의에서 연습문제가 많아서 따로 프로그래머스 문제 과제는 없습니다.)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | ✅         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>



<!-- 여기까진 그대로 둬 주세요-->

---

# 4-4. 날짜 및 시간 데이터 이해하기(2) (EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME)

~~~
✅ 학습 목표 :
* 날짜 및 시간 데이터에 대해서 더 자세히 설명할 수 있다. 
* CURRENT_TIME, EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME 을 설명할 수 있다. 
~~~

<날짜 및 시간 데이터 타입>

DATE : 날짜만 저장
DATETIME : 날짜 + 시간 (타임존 X)
TIMESTAMP : 날짜 + 시간 (UTC 기준, 타임존 O)
UTC : 세계 표준시 (한국 = UTC+9)
Millisecond : 1/1000초
Microsecond : 1/1000ms

DATETIME vs TIMESTAMP

DATETIME : 타임존 영향 없음 → 한국 기준 데이터 처리에 직관적
TIMESTAMP : UTC 기준 → 한국 시간 사용 시 +9시간 고려 필요

<CURRENT_DATETIME>

현재 날짜 + 시간 반환
타임존 지정 가능

CURRENT_DATETIME()
CURRENT_DATETIME("Asia/Seoul")

<EXTRACT (특정 값 추출)>

DATETIME에서 필요한 부분만 뽑기

EXTRACT(YEAR FROM datetime)
EXTRACT(MONTH FROM datetime)
EXTRACT(DAY FROM datetime)
EXTRACT(HOUR FROM datetime)
EXTRACT(MINUTE FROM datetime)

- 요일 추출
EXTRACT(DAYOFWEEK FROM datetime)

일요일 = 1 ~ 토요일 = 7

<전체 흐름 정리>

현재 시간 : CURRENT_DATETIME
부분 추출 : EXTRACT
단위 기준 정리 : DATETIME_TRUNC
타입 변환
문자열 → DATETIME : PARSE_DATETIME
DATETIME → 문자열 : FORMAT_DATETIME
기간 계산
마지막 날짜 : LAST_DAY
시간 차이 : DATETIME_DIFF

# 4-6. 조건문(CASE WHEN, IF)

~~~
✅ 학습 목표 :
* 조건문 함수의 기능을 이해하고, 설명할 수 있다. 
~~~

<조건문 개념>

특정 조건을 기준으로 서로 다른 값을 반환하는 문법
데이터 분류, 범주화, 새로운 컬럼 생성에 활용

<CASE WHEN (다중 조건 처리)>

여러 조건을 순서대로 검사하여 결과 반환
조건이 많거나 복잡할 때 사용

SELECT
CASE
WHEN 조건1 THEN 결과1
WHEN 조건2 THEN 결과2
ELSE 그 외 결과
END AS 새로운_컬럼
위에서부터 순서대로 평가
여러 조건에 해당해도 먼저 만족한 조건이 적용됨

<IF (단일 조건 처리)>

하나의 조건을 기준으로 두 가지 결과 중 선택

IF(조건, TRUE일 때 값, FALSE일 때 값) AS 새로운_컬럼

 # 4-5. 시간 데이터 연습문제 & 4-7. 조건문 연습 문제

~~~
✅ 학습 목표 :
* 4-5, 4-7 각각에서 두 문제 이상 (최소 4문제) 푼 내용 정리하기
~~~

문제 1
트레이너가 포켓몬을 포획한 날짜(catch_date)를 기준으로, 2023년 1월에 포획한 포켓몬의 수를 계산

SELECT 
  COUNT(DISTINCT id) AS cnt
FROM basic.trainer_pokemon
WHERE
  EXTRACT(YEAR FROM DATETIME(catch_datetime, "Asia/Seoul")) = 2023
  AND EXTRACT(MONTH FROM DATETIME(catch_datetime, "Asia/Seoul")) = 1

- catch_datetime이 TIMESTAMP라서 DATETIME으로 변환 후 사용
- 연도와 월을 EXTRACT로 분리해서 조건 설정

문제 2
배틀이 일어난 날짜(battle_date)를 기준으로, 요일별 배틀 횟수 계산

SELECT
  day_of_week,
  COUNT(DISTINCT id) AS battle_cnt
FROM (
   SELECT
     *,
     EXTRACT(DAYOFWEEK FROM battle_date) AS day_of_week
   FROM basic.battle
   )
GROUP BY
  day_of_week
ORDER BY
  day_of_week

- EXTRACT(DAYOFWEEK)로 요일 숫자 추출
- 서브쿼리로 컬럼 생성 후 그룹화

문제 3
포켓몬의 speed가 70 이상이면 '빠름', 아니면 '느림'으로 분류

SELECT
 id,
 kor_name,
 speed,
 IF(speed >= 70, "빠름", "느림") AS Speed_Category
FROM basic.pokemon

- 단일 조건이므로 IF 사용
- 조건에 따라 값 분기

문제 4
포켓몬 type1을 한글로 변환

SELECT
 id,
 kor_name,
 type1,
 CASE
  WHEN type1 = "Water" THEN "물"
  WHEN type1 = "Fire" THEN "불"
  WHEN type1 = "Electric" THEN "전기"
  ELSE "기타"
 END AS type1_Korean
FROM basic.pokemon

- 여러 조건이므로 CASE WHEN 사용
- 조건 순서대로 매칭

깨달은 점

- TIMESTAMP 데이터는 그대로 쓰면 오류 발생 가능 → DATETIME 변환 필요
- 시간 데이터는 EXTRACT로 쪼개서 조건 설정하는 게 핵심
- 조건이 하나면 IF, 여러 개면 CASE WHEN이 더 적절
- 데이터 변환 및 분류는 새로운 컬럼 생성 방식으로 처리하는 것이 효율적

<br>

<br>

---

# 확인문제

## 문제 1

> **🧚Q. 광윤이는 카페 주문 로그 데이터(order_log)를 분석하여, '오전(0시-11시)'과 '오후(12시-23시)'의 주문 건수를 집계하려고 합니다. 광윤이가 작성한 다음 SQL 쿼리 중 문법적으로 틀렸거나 의도한 결과가 나오지 않는 것을 모두 골라보세요. (복수 선택 가능)**

~~~sql
1. SELECT 
   IF(EXTRACT(HOUR FROM order_time) < 12, '오전', '오후') AS time_type,
   COUNT(*)
   FROM order_log
   GROUP BY time_type;

2. SELECT 
   DATETIME_TRUNC(order_time, HOUR) AS truncated_hour,
   COUNT(*)
   FROM order_log
   WHERE order_time BETWEEN '2021-01-01' AND '2021-12-31'
   GROUP BY order_time;

3. SELECT 
   FORMAT_DATETIME(order_time, '%H') AS order_hour,
   COUNT(*)
   FROM order_log
   GROUP BY 1;

4. SELECT 
    CASE 
      WHEN EXTRACT(HOUR FROM order_time) BETWEEN 0 AND 11 THEN '오전'
      ELSE '오후'
    AS time_group,
    COUNT(*)
   FROM order_log
   GROUP BY time_group;
~~~

<!-- 틀린쿼리에 대한 오류의 원인도 같이 작성해주세요. 문제에서 제공된 order_time 컬럼은 DATETIME type의 데이터를 가지고 있다고 가정합니다. -->

<정답>
2,4번

- 2번 오류 이유

DATETIME_TRUNC(order_time, HOUR) AS truncated_hour

로 시간 단위를 잘라놓고,

GROUP BY order_time

으로 원본 컬럼을 기준으로 그룹화하고 있음

→ SELECT와 GROUP BY 기준이 다르기 때문에 의도한 결과(시간 단위 집계)가 나오지 않음
→ GROUP BY truncated_hour 또는 GROUP BY 1로 수정해야 함

- 4번 오류 이유

CASE 
  WHEN EXTRACT(HOUR FROM order_time) BETWEEN 0 AND 11 THEN '오전'
  ELSE '오후'
AS time_group

→ CASE 문에 END가 없음 → 문법 오류

- 올바른 형태:
CASE 
  WHEN EXTRACT(HOUR FROM order_time) BETWEEN 0 AND 11 THEN '오전'
  ELSE '오후'
END AS time_group



## 문제 2

> **🧚Q. 예운이는 포켓몬 타입에 따라 설명을 부여하는 쿼리를 작성했습니다. type 1 컬럼의 값에 따라 조건을 분기했으며, 다음 SQL 쿼리를 실행했습니다.**

~~~sql
SELECT name,
       CASE 
         WHEN type1 = 'Fire' THEN 'Hot'
         WHEN type1 = 'Water' THEN 'Cool'
         ELSE 'Normal'
       END AS type_description
FROM pokemon;
~~~

> **다음 중 type_description의 결과가 'Normal'로 출력될 포켓몬은?**

| **name**   | **type1** |
| ---------- | --------- |
| Pikachu    | Electric  |
| Charmander | Fire      |
| Squirtle   | Water     |
| Bulbasaur  | Grass     |

<!-- 근거와 함께 답을 작성해주세요 -->

<정답>
Pikachu, Bulbasaur

- 이유

CASE 
  WHEN type1 = 'Fire' THEN 'Hot'
  WHEN type1 = 'Water' THEN 'Cool'
  ELSE 'Normal'
END
Fire → Hot
Water → Cool
그 외 → Normal

- 각 포켓몬 결과

Pikachu (Electric) → 조건 없음 → Normal
Charmander (Fire) → Hot
Squirtle (Water) → Cool
Bulbasaur (Grass) → 조건 없음 → Normal

<br>

### 🎉 수고하셨습니다.
