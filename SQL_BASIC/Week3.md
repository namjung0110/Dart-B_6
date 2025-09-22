# SQL_BASIC 3주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_3rd_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**3주차 과제는 문제 풀이를 중심으로**, 강의에서 제시된 예제 문제 중 **7 문제 이상을 선택하여 직접 풀어본 뒤**, 강의 영상의 풀이와 비교해 **틀린 부분, 맞은 부분, 새롭게 배운 개념**을 구체적으로 정리해주세요. (적어도 3문제는 정리해야 합니다.) 완성된 과제는 Gihub에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_3rd

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-6. 연습문제 1~3번

### 2-6. 연습문제 7~9번

### 2-6. 연습문제 10~12번

### 2-6. 연습문제 13~17번

### 2-7. 정리 

### 2-8. 새로운 집계함수



## 섹션 4. 쿼리 잘 작성하기, 쿼리 작성 템플릿 및 오류를 잘 디버깅하기

### 3-1. INTRO

### 3-2. SQL 쿼리 작성하는 흐름

### 3-3. 쿼리 작성 템플릿과 생산성 도구 



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | 🍽️         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리

## 2-6. 연습문제

~~~
✅ 학습 목표 :
* 연습문제(7문제 이상) 푼 것들 정리하기
~~~

---

## NULL이란?

 >값이 없는 상태를 말함

=> 0, 비어있는 문자열과 다름

>ex ) TYPE2 IS NULL

특징 1. IS 연산자 사용

특징2. 다른 값과 직접 비교가 안됨

## 문제 1 
포켓몬 중에 type2 가 없는 포켓몬의 수를 작성하는 쿼리

~~~
SELECT  
  COUNT(id) AS cnt
FROM basic.pokemon 
WHERE 
 (type2 IS NULL)
 OR (type1 =  "Fire") 

~~~

## 문제 2
type2가 없는 포켓몬의 type1과 type1의 포켓몬 수를 알려주는 쿼리

~~~
SELECT
  type1
  COUNT(id) AS pokemon_cnt
FROM basic.pokemon
WHERE
  type2 IS NULL 
GROUP BY
  type1
ORDER BY
  pokemon_cnt DESC
~~~
## 문제 3
 type2 상관없이 type1의 포켓몬 수를 알 수 있는 쿼리를 작성

~~~
SELECT
   type1,
   COUNT(id) AS pokemon_cnt
   COUNT(DISTINCT id) AS pokemon_cnt2
FROM basic.pokemon
~~~

## 문제 4
전설 여부에 따른 포켓몬 수를 알 수 있는 쿼리를 작성

~~~
SELECT 
   is_legendary 
   COUNT(id) AS pokemon_cnt 
FROM basic.pokemon 
GROUP BY 
    is_legendary
~~~

## 문제 5
동명이인이 있는 이름

~~~
SELECT 
  name      
  COUNT(name) AS trainer_cnt 
FROM basic.trainer 
GROUP BY 
  name 
HAVING 
  trainer_cnt
~~~

## 문제 6
trainer 테이블에서 "Iris"트레이너의 정보를 알 수 있는 쿼리

~~~
SELECT 
    * 
FROM basic.trainer 
WHERE 
    name = "Iris"
~~~

## 문제 7
trainer 테이블에서 "Iris" "Whitney" "Cynthia" 트레이너의 정보를 알 수 있는 쿼리 작성

~~~
SELECT 
   * 
FROM basic.trainer 
WHERE 
   (name = "Iris") 
   OR (name = "Whitney") 
   OR (name = "Cynthia")
~~~

## 문제 8
전체 포켓몬 수?

~~~
SELECT 
   COUNT(id) AS pokemon_cnt 
FROM basic.pokemon
~~~

## 문제 9
세대별로 포켓몬 수가 얼마나 되는지 알 수 있는 쿼리

~~~
SELECT 
    generation 
    COUNT(id) AS pokemon_cnt 
FROM basic.pokemon 
GROUP BY 
    generation
~~~

## 문제 10
type2가 존재하는 포켓몬의 수

~~~
SELECT 
   COUNT(id) AS pokemon_cnt 
FROM basic.pokemon 
WHERE 
   type2 IS NOT NULL
~~~

## 문제 11
type2 가 있는 포켓몬 중에 제일 많은 type1

~~~
SELECT 
   type1 
   COUNT(id) AS pokemon_cnt 
FROM basic.pokemoon 
WHERE 
   type2 IS NOT NULL 
GROUP BY 
   type1 
ORDER BY 
   pokemon_cnt 
DESC LIMIT 1
~~~

## 문제 12
단일타입 포켓몬 중 많은 type1

~~~
SELECT 
   type1 
   COUNT(id) AS pokemon_cnt 
FROM basic.pokemon 
WHERE 
   type2 IS NOT NULL 
GROUP BY 
   type1 
ORDER BY 
   pokemon_cnt 
DESC LIMIT1
~~~

## 문제 13
포켓몬의 이름에 '파'가 들어가는 포켓몬

~~~
SELECT 
   kor_name 
FROM basic.pokemon 
WHERE 
   name LIKE "파%"
~~~

## 문제 14
뱃지가 6개 이상인 트레이너

~~~
SELECT 
   COUNT(id) AS trainer_cnt 
FROM basic.trainer 
WHERE 
   badge_count >= 6
~~~

## 문제 15
트레이너가 보유한 포켓몬이 제일 많은 트레이너

~~~
SELECT 
   trianer_id 
   COUNT(trianer_id) AS pokemon_cnt 
FROM basic.trianer_pokemon 
GROUP BY 
   trainer_id
~~~

## 문제 16
포켓몬을 많이 풀어준 트레이너

~~~
SELECT 
   trainer_id 
   COUNT(pokemon_id) AS pokemon_cnt 
FROM basic.trainer_pokemon 
WHERE 
   status = " Released" 
GROUP BY 
   trainer_id 
ORDER BY 
   pokemon_cnt 
DESC LIMIT 1
~~~

## 문제 17
트레이너 별로 풀어준 포켓몬의 비율이 20%가 넘는 포켓몬 트레이너

~~~
SELECT 
   COUNT IF(status = "Released") AS released_cnt 
   COUNT(pokemon_id) AS pokemon_cnt 
   COUNTIF(status = "Released")/COUNT(pokemon_id) As released_ratio 
FROM basic.trainer_pokemon 
GROUP BY 
   trainer_id 
HAVING 
   released_ratio >= 0.2
~~~

## 2-8. 새로운 집계함수

~~~
✅ 학습 목표 :
* SQL 쿼리 구조를 이해할 수 있다. 
* SELECT, FROM, WHERE을 활용하는 방법을 설명할 수 있다. 
~~~

## GROUP BY ALL
>GROUP BY  컬럼을 명시해줬어야하는 데 이제 GROUP BY ALL 사용 가능

즉, 그룹화할 키를 inferring 해서 추론,자동으로 GROUP BY a,b,c, 사용 없이 GROUP BY ALL로 가능하도록 해줌

## 3-2. 쿼리를 작성하는 흐름

~~~
✅ 학습 목표 :
* 쿼리를 작성하는 흐름을 설명할 수 있다.
~~~

~~~
지표고민 : 어떤 문제를 해결하기 위해 데이터가 필요한가?

지표 구체화 : 추상적이지 않고 구체적인 지표 명시(분자 분모 표시)

지표 탐색 : 유사한 문제를 해결한 케이스가 있나 확인 

=> 존재한다면 해당 쿼리 리뷰

쿼리 작성 : 데이터가 있는 테이블 찾기

=> 1개 : 활용 
   2개 이상 : 연결 방법 고민(JOIN)

데이터 적합성 확인 : 예상한 결과와 동일한지 확인

쿼리 가독성 : 나중을 위해 깔끔하게 쿼리 작성

쿼리 저징 : 쿼리가 재사용되므로 문서로 저장
~~~

namjung0110/Dart-B_6/images/image copy 8.png


## 3-3. 쿼리 작성 템플릿과 생산성 도구

~~~
✅ 학습 목표 :
* 생산성 도구를 만들 수 있다.
~~~

관리자 권한으로 실행해봐도 안되네요...

<br>
<br>

---

# 2️⃣ 학습 인증란

![namjung0110/Dart-B_6/images/인증.PNG](인증.PNG)

<br><br>



---

# 3️⃣ 확인문제

## 문제 1

> **🧚Q. 포켓몬 게임에 재미를 느낀 동혁은 포켓몬 도감에서 강력한 포켓몬 타입을 미리 선점하기 위해, 먼저 어떤 포켓몬들이 있는지 포켓몬 수를 기준으로 내림차순 정렬하여  확인하고자 했습니다.**
>
> 그래서 다음과 같은 필요한 정보를 미리 정리해보았습니다. 

~~~
조건 : type2는 상관없이
보고 싶은 컬럼 : type1
집계 내용 : 각 type1 별 포켓몬 수
정렬 기준 : 포켓몬 수를 기준으로 내림차순 정렬
~~~

> **이 목표를 바탕으로 동혁이 아래와 같은 쿼리를 잘 작성했지만, 일부 SQL 문법 요소를 빼먹었습니다. 비어 있는 부분인 ㄱ,ㄴ,ㄷ 에 들어갈 알맞은 SQL 구문을 채워보세요:**

~~~sql
SELECT type1, (ㄱ)
FROM pokemon
(ㄴ) type1
ORDER BY (ㄱ) (ㄷ);
~~~



~~~
ㄱ : COUNT *
ㄴ : GROUP BY
ㄷ : DESC
~~~



### 🎉 수고하셨습니다.