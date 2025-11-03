# SQL_BASIC 5주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_5th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**5주차 과제는 문제 풀이를 중심으로**, 강의에서 제시된 예제 문제 중 **3 문제 이상을 선택하여 직접 풀어본 뒤**, 강의 영상의 풀이와 비교해 **틀린 부분, 맞은 부분, 새롭게 배운 개념**을 구체적으로 정리해주세요. (적어도 4문제는 정리해야 합니다.) 완성된 과제는 Gihub에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 

![alt text](<../images/image copy 22.png>)

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

## 날짜 및 시간 데이터 타입 파악하기

DATE : 날짜만 표시하는 데이터
>- 시간 분 초 없음 

DATETIME: 날짜와 시간까지 표시하는 데이터
>-tIME zONE 정보 없음
TIME: 날짜와 무관하게 시간만 표시하는 데이터

## 타임존

GMT : 영국 그리니치 천문대를 기준으로 지역에 따른 시간의 차이를 조정하기 위해 생긴 시간의 구분선

UTC : 국제적인 표준 시간 (GMT와 유사하다고 생각하면 된다)
>-타임존이 존재한다 = 특정 지역의 표준 시간대

-- TIMESTAMP --
시간 도장
UTC부터 경과한 시간을 나타내는 값
Time Zone 정보있음

## 시간 데이터 다룩

--millisecond(ms)--

천 분의 1초
>-빠른 반응이 필요한 분야에서 사용(초보다 더 정확하게)

--microsecond(us)--

1/1000 millisecond

## EXTRACT
DATETIME에서 특정 부분만 추출하고 싶은 경우
>-EXTRACT (DAYOFWEEK FROM datetime_col)

## DATTIME_TRUNC

일부만 남기고 싶을 때

예시

DATE와 HOUR만 남기고 싶은 경우 
DATETIME_TRUNC (DATETIME "2024-03-02 14:42:13",HOUR) AS hour_trunc

## PARSE_DATETIME

문자열로 저장된 DATETIME을 DATETIME 타입으로 바꾸고 싶은 경우

PARSE_DATETIME('문자열의 형태','DATETIME 문자열') AS datetime

## FORMAT_DATETIME

DATETIME 타입 데이터를 특정 형태의 문자열 데이터로 변환하고 싶은 경우

## LAST_DAY

마지막 날을 알고 싶은 경우 : 자동으로 월의 마지막 값을 계산해서 특정 연산을 할 경우

LAST_DAY(DATETIME) : 월의 마지막 값을 반환

## DATETIME_DIFF

두 DATETIME의 차이를 알고 싶은 경우

DATETIME_DIFF(첫 DATETIME , 두번째 DATETIME, 궁금한 차이)

예시

DATETIME_DIFF(first_datetime,second_datetime, DAY) AS day_diff1

# 4-6. 조건문(CASE WHEN, IF)

~~~
✅ 학습 목표 :
* 조건문 함수의 기능을 이해하고, 설명할 수 있다. 
~~~

## 조건문 

만약 특정 조건이 충족되면 어떤 행동을 하자

특정 조건이 참일 때 A, 아니면 B
  >- 조건에 따른 분기 처리가 필요한 경우

조건에 따라 다른 값을 표시하고 싶을 때 사용

## 조건문 함수가 사용되는 이유

특정 카테코리를 하나로 합치는 전처리가  필요할 수 있음.

>- 1. 데이터를 저장하는 쪽과 데이터를 분석하는 쪽이 나뉨.

>- 2. 분석할 떄 필요한 부분에서 조건 설정해서 변경하는 것이 더 유용

>- 3. 저장할 때부터 특정 카테고리를 합쳐서 저장하면, 쪼개서 보고 싶을 떄 볼 수 있음.

## CASE WHEN

여러 조건이 있을 경우 유용

--문법--
~~~
SELECT

  CASE
   WHEN 조건 1 THEN 조건 1이 참일 경우 결과
   ELSE 그 외 조건일 경우 결과
END AS 새로운 컬럼_이름

~~~
## IF

단일 조건일 경우 유용

문법 
-IF(조건문,True일 때의 값 , False일 때의 값) AS 새로운_컬럼_이름
 # 4-5. 시간 데이터 연습문제 & 4-7. 조건문 연습 문제

~~~
✅ 학습 목표 :
* 4-5, 4-7 각각에서 두 문제 이상 (최소 4문제) 푼 내용 정리하기
~~~

## 4-5-3

1. 각 트레이너별로 그들이 포켓몬을 포획한 첫 날을 찾고, 그 날짜를 'DD/MM/YYYY' 형식으로 출력해주세요

쿼리를 작성하는 목표, 확인할 지표 : 날짜를 특정 형태로 변경! + 포획한 첫 날

쿼리 계산 방법 : DATE ==> 문자열 , FORMAT_DATETIME + MIN

데이터 기간 : X

사용할 테이블 : trainer_pokemon

Join KEY : X

데이터 특징 : catch_date는 UTC 기준의 데이터. 한국 기준으로 하려면 catch_datetime을 사용해야 한다.

~~~
SELECT
  trainer_id
  FORMAT_DATE("%d%m/Y%", min_catch_date)
FROM (
    SELECT
      trainer_id,
      MIN(DATE(catch_datetime , "Asia/Seoul" )) AS min_catch_date
      FROM basic.
      GROUP BY
        trainer_id
      ORDER BY
        trainer_id
)
~~~

4-5-4

2. 배틀이 일어난 날짜를 기준으로 요일별로 배틀이 얼마나 자주 일어났는 지 계산해주세요

쿼리를 작성하는 목표, 확인할 지표 : 요일별로 배틀이 얼마나 자주 일어났는가? 

쿼리 계산 방법 : 요일별로 COUNT

데이터의 기간 : X

사용할 테이블 : battle

Join KEY : X

데이터 특징 : battle_date가 정상적임

~~~
SELECT
  day_of_week,
  COUNT(DISTINCT id) AS battle_cnt
FROM (
  SELECT
   *
   EXTRACT(DAYOFWEEK FROM battle_date) AS day_of_week
  FROM basic.battle
)
GROUP BY
  day_of_week
ORDER BY
  day_of_week
~~~

4-7-2

3. 포켓몬의 'type1'에 따라 'Water','Fire','Electric' 타입은 각각 '물','불','전기'로 그 외의 타입은 기타로 분류하는 새로운 칼럼 'type_Korean' 을 만들어 주세요

쿼리를 작성하는 목표, 확인할 지표 : type1을 사용해서 특정 조건을 만족하는 것은 값을 변경, 기타 => type_Korean

쿼리 계산 방법  : CASE WHEN , IF =>  여러조건이 있음. Water ==> 물 , Fire => 불  Electric => 전기

데이터 기간 : X

사용자 테이블 : pokemon

Join KEY : X

~~~
SELECT
  id,
  kor_name,
  type1,
  CASE
   WHEN type1 =  "Water" THEN "물"
   WHEN type1 = "Fire" THEN "불"
   WHEN type1 =  "Electric" THEN "전기"
   ELSE "기타"
  END AS type1_Korean
FROM basic.pokemon
~~~
4-7-3

4. 각 포켓몬의 총점(total)을 기준ㅇ르ㅗ, 300 이하면 'Low', 301 에서 500 사이면 'Medium', 501 이상이면 'High'로 분류해주세요

쿼리를 작성하는 목표, 확인할 지표 : total 컬럼 => 조건에 맞는 값을 변경! 모두 다 숫자!

쿼리 계산 방법 : CASE WHEN

데이터의 기간 : X

사용할 테이블 : pokemon

Join KEY : X

데이터 특징 : total  컬럼이 정수(INTEGER)

~~~
SELECT
 id,
 kor_name,
 total,
 CASE
   WHEN total >= 501 THEN "High" 
   WHEN total BETWEEN 300 AND 500 THEN "Medium"  
 ELSE "Low"
 END AS total_grade
FROM basic.pokemon
WHERE
 total_grade = "Low"
~~~
<br>

<br>

---

# 확인문제

## 문제 1

> **🧚Q. 광윤이는 사용자 로그 데이터에서, 2021년에 접속한 사용자 수를  집계하려고 했습니다. 그는 여러 SQL 쿼리들을 실행해봤지만, 그 중 일부는 문법적으로 잘못되어 실행되지 않았습니다. 다음 보기 중 틀린 쿼리를 모두 골라보세요 (복수 선택 가능)**

~~~sql
1. SELECT COUNT(*)  
   FROM user_log  
   WHERE EXTRACT(YEAR FROM login_date) = 2021;

2. SELECT EXTRACT(YEAR FROM login_date), COUNT(*)  
   FROM user_log  
   GROUP BY EXTRACT(YEAR FROM login_date);

3. SELECT COUNT(*)  
   FROM user_log  
   WHERE login_date = '2021';

4. SELECT COUNT(*)  
   FROM user_log  
   WHERE login_date BETWEEN '2021-01-01' AND '2021-12-31';
~~~

<!-- 틀린쿼리에 대한 오류의 원인도 같이 작성해주세요. 문제에서 제공된 login_data 컬럼은 DATE type의 데이터를 가지고 있다고 가정하시면 됩니다. -->

~~~
(3) 

오류가 발생하는 이유는 login_date 컬럼이 DATE 타입이기 때문이다.
DATE 타입 컬럼에 값을 입력할 때는 반드시 유효한 날짜 형식이어야 하며,'2021'은 연도만 입력한 문자열은 올바른 날짜로 인식되지 않는다.
~~~



## 문제 2

> **🧚Q. 혜성이는 포켓몬 타입에 따라 설명을 부여하는 쿼리를 작성했습니다. type 1 컬럼의 값에 따라 조건을 분기했으며, 다음 SQL 쿼리를 실행했습니다.**

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

~~~
Pikachu, Bulbasaur

type1 값이 'Electric'인 Pikachu와 'Grass' 타입인 Bulbasaur는 어느 조건에도 일치하지 않기 때문에 결과가 자동으로 'Normal'로 분류된다.
~~~



<br>

### 🎉 수고하셨습니다.