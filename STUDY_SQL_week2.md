## SQL 스터디 2주차 과제

### 석민주
```SQL
SELECT T.ITEM_ID,
       I.ITEM_NAME
FROM ITEM_TREE T
JOIN ITEM_INFO I on I.ITEM_ID=T.ITEM_ID
WHERE T.PARENT_ITEM_ID IS NULL
```

### 국지희
```SQL
SELECT BOARD_ID,
       WRITER_ID,
       TITLE,
       PRICE,
       CASE
        WHEN STATUS LIKE 'SALE' THEN '판매중'
        WHEN STATUS LIKE 'RESERVED' THEN '예약중'
        WHEN STATUS LIKE 'DONE' THEN '거래완료'
       END AS STATUS
FROM USED_GOODS_BOARD
WHERE DATE(CREATED_DATE) = "2022-10-05"
ORDER BY BOARD_ID DESC
```

### 유현
```SQL
SELECT
    ROUTE,
    CONCAT(ROUND(SUM(D_BETWEEN_DIST), 1), 'km') AS TOTAL_DISTANCE,
    CONCAT(ROUND(AVG(D_BETWEEN_DIST), 2), 'km') AS AVERAGE_DISTANCE
FROM SUBWAY_DISTANCE
GROUP BY ROUTE
ORDER BY SUM(D_BETWEEN_DIST) DESC;
```
<!-- ROUND 함수는 명시된 자리까지 반올림-->

### 이승화
```SQL
SELECT
    ORDER_ID,
    PRODUCT_ID,
    DATE_FORMAT(OUT_DATE, '%Y-%m-%d'),
    CASE
        WHEN DATEDIFF(OUT_DATE, '2022-05-01') > 0 THEN '출고대기'
        WHEN DATEDIFF(OUT_DATE, '2022-05-01') <= 0 THEN '출고완료'
        ELSE '출고미정'
    END AS 출고여부
FROM
    FOOD_ORDER
ORDER BY
    ORDER_ID ASC
```


### 새로 배운 개념

- CASE 문
```SQL
CASE 
        WHEN STATUS LIKE 'A' THEN 'B'
        WHEN '수식' THEN 'C'
  END AS 칼럼이름
```
 : A일 때 B 출력,
   수식에 만족할 때 C 출력

- CONTCAT 함수 : 문자열을 이어줌
