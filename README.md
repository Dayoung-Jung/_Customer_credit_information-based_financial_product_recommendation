# _Customer_credit_information-based_financial_product_recommendation

---

## 과제 목적

1. 고객 신용 정보 기반으로 대출 신청자 예측 모델 개발
2. 고객 카드 정보 등을 통해, 대출 상품 추천
3. 고객 신용 정보 및 추천된 상품을 확인할 수 있는 고객 포트폴리오 대시보드 설계 및 제안

---

## 과제 수행방법

### 1. 데이터
    - 금융 빅데이터 개방시스템(CreDB)에 등록된 고객 대출 및 신용 정보 데이터
    - 데이터는 예측과 추천시스템 각 프로세스에 맞춰 사용할 테이블을 추출하고, 테이블 내의 데이터들도 전처리하는 과정을 통해 준비
    - 데이터의 불균형 문제와 실험적인 비교를 위하여 over, under sampling 진행
### 2. 예측
    - 두가지 논문에 기반하여 XGBoost, random forest 등의 bagging, boosting 모델들을 사용해 정확도를 비교하는 과정 진행
    - raw data, over, under sampling data들에 대하여 각각 모델들을 학습
    - precision, recall, F1 score를 비교하여 데이터와 모델 채택
    - 채택된 모델은 grid search cv를 통해 하이퍼파라미터 조정과 cross validation까지 진행
### 3. 추천
    - 유저들간의 cosine similarity를 구하고 cosine similarity가 높은 Topk명을 추출
    - k명의 사람들이 가장 많이 신청한 상품을 선정하여 추천하는 방식으로 프로세스 구축

---

## 최종 결과물 주요 특징 및 설명
### 1. 대출 신청자 예측
       1) 진행한 예측 모델: CART, CHAID, C4.5, RF, GBM, XGBoost, LGBM
       2) 진행한 데이터: raw data, under sampling data, over sampling data
       3) 최종 결론 예측 모델: XGBoost
       4) 최종 결론 예측 데이터: over sampling data
       5) 예측 성능도: 78%
       6) shap 기법을 기반으로 유의미한 feature 추출 35개 추출

### 2. 고객 금융 상품 추천
        1) 사용한 추천 데이터: 사용한 카드 정보 데이터
        2) 사용한 추천 모델: 코사인 유사 측정 & TOP K 명 추출
        3) 추천 성능도: TOP 80명에 대해서, 37%
        4) 추천 결과물
           - 개인: 대출 상품, 대출 금액 최소/최대, 대출 금리 최대/최소
           - 개인 사업자: 대출 상품, 대출 금액 최소/최대

### 3. 예측과 추천 기반 고객 포트폴리오
       1) 개인 고객 금융 정보
          - 업권코드
          - 신용/체크 카드 개수, 신용/체크 한도 및 평균 사용 금액
          - 금융기관 & 공공기관: 연체금액 최대/평균/최소, 연체 사유별 유무, 연체 총 횟수
       2) 개인 고객 금융 추천 페이지
          - 고객 정보, 대출 상품 추천 및 관련 금액과 금리 정보
          - 대출 상품 리스트
          - 전체 고객의 대출 금액 Max – Min 분포도
          - 전체 고객의 금리 Max – Min 분포도
       3) 개인 사업자 고객 금융 정보
          - 업권코드
          - 신용/체크 카드 개수, 신용/체크 한도 및 평균 사용 금액
          - 금융기관 & 공공기관: 연체금액 최대/평균/최소, 연체 사유별 유무, 연체 총 횟수
       4) 개인 사업자 고객 금융 추천 페이지
          - 고객 정보, 대출 상품 추천 및 관련 금액 정보
          - 고객이 종사하는 업종 코드
          - 전체 고객의 대출 금액 Max – Min 분포도
---
