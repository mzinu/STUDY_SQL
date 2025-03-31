## SQL 스터디 1주차 과제

### 석민주
SELECT 
    B.TITLE,
    B.BOARD_ID,
    R.REPLY_ID, 
    R.WRITER_ID, 
    R.CONTENTS, 
    DATE_FORMAT(R.CREATED_DATE, '%Y-%m-%d') --CREATED_DATE의 데이터 타입은 시간포함이라 날짜로 바꿔줌
    CREATED_DATE
from USED_GOODS_BOARD B --테이블 별칭 설정
inner join USED_GOODS_REPLY R on B.BOARD_ID = R.BOARD_ID
where B.CREATED_DATE LIKE '2022-10%' --2022-10으로 시작하는 값만 찾기. %는 데이터포맷 코드 종류이자 와일드키
order by CREATED_DATE asc, 
         TITLE asc;


### 국지희
SELECT 
    DATE(order_delivered_carrier_date) AS delivered_carrier_date,
    COUNT(*) AS orders
FROM olist_orders_dataset
WHERE order_delivered_carrier_date LIKE '2017-01%'
AND order_delivered_customer_date IS NULL
GROUP BY DATE(order_delivered_carrier_date)
ORDER BY delivered_carrier_date ASC;


### 유현

SELECT DATE(o.order_purchase_timestamp) AS dt,
       ROUND(SUM(op.payment_value),2) AS revenue_daily
FROM olist_orders_dataset o 
JOIN olist_order_payments_dataset op on o.order_id = op.order_id
WHERE dt >= '2018-01-01' 
GROUP BY DATE(o.order_purchase_timestamp)
ORDER BY dt ASC;


### 이상화

SELECT 
    E.ID,  
    E.GENOTYPE,  
    P.GENOTYPE AS PARENT_GENOTYPE  
FROM ECOLI_DATA E  
LEFT JOIN ECOLI_DATA P ON E.PARENT_ID = P.ID  
WHERE E.PARENT_ID IS NOT NULL 
     AND (E.GENOTYPE & P.GENOTYPE) 
     

## 핵심개념

### LIKE 연산자

LIKE 와일드카드(%, _) 사용법

패턴	                설명            	           예시 (매칭됨)	       예시 (매칭안됨)

'2022-10%'  	2022년 10월로 시작하는 값 찾기	   2022-10-15 08:00:00	    2022-09-30 23:59:59

'%2022%'	    2022가 포함된 값 찾기	              상품 2022 버전	        상품 2023 버전

'2022-10-__'	2022년 10월 "특정 일" 찾기	           2022-10-15	              2022-10

➡ % : 0개 이상의 모든 문자 가능 

➡ _ : 정확히 한 글자만 채워짐

### DATE_FORMAT()

포맷 코드	설명	        예시 (2022-10-05 14:23:11)

%Y     	4자리 연도	                2022

%y     	2자리 연도	                22

%m	    월 (2자리)	                10

%d  	일 (2자리)	                05

%H  	시 (24시간제)	            14

%i	    분	                        23

%s  	초	                        11

%W  	요일 (영어)              Wednesday

%a	    요일 (축약형)	            Wed
