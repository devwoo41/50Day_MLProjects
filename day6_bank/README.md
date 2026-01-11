# Bank Marketing Data Analysis & Prediction Project

본 프로젝트는 은행 마케팅 데이터를 분석하여 고객의 정기 예금(term deposit) 가입 여부를 예측하는 모델을 개발하는 것을 목표로 합니다.

## 1. 탐색적 데이터 분석 (EDA) 요약
`EDA.ipynb`에서는 데이터의 기본적인 분포와 목표 변수(`y`: 정기 예금 가입 여부)와의 관계를 분석하였습니다.

### 주요 발견 사항
- **통장 잔고 (Balance)**: 정기 예금 가입자 그룹의 평균 통장 잔고가 비가입자 그룹보다 소폭 높은 경향이 있습니다.
- **연령 (Age)**:
  - 가입자는 30세 미만의 젊은 층과 60세 이상의 고연령층 비율이 상대적으로 높습니다.
  - 비가입자는 30~50대(경제활동 주력 계층)의 비율이 높습니다.
- **직업 (Job)**: `management`(경영직), `retired`(은퇴자), `student`(학생) 직군에서 가입 비율이 상대적으로 높게 나타났습니다.
- **결혼 상태 (Marital)**: `single`(미혼)인 경우 가입 비율이 상대적으로 높습니다.
- **교육 수준 (Education)**: `tertiary`(고등 교육 이수) 그룹의 가입 비중이 높습니다.
- **캠페인 연락 (Campaign & Pdays)**:
  - 이번 캠페인 기간 동안의 연락 횟수(`campaign`)는 비가입자가 평균적으로 더 많았습니다.
  - 이전 연락 후 경과일(`pdays`) 분석 결과, 오랜 기간 연락이 없었던 고객들이 비가입자 그룹에 많이 분포하는 것으로 보입니다.

---

## 2. 예측 모델링 (Modeling) 요약
`Train.ipynb`에서는 데이터 전처리, 특성 공학, 그리고 머신러닝 모델 학습 및 평가를 진행하였습니다.

### 데이터 전처리 및 특성 공학
- **결측치 및 중복 제거**: 데이터 정제 수행.
- **파생 변수 생성**: `pdays` 변수를 범주화하여 `pdays_cat` ('연락x', '100일 이내' 등) 생성.
- **인코딩**: 범주형 변수(Categorical features)에 대해 One-Hot Encoding 적용.
- **데이터 분할**: 학습용(Train)과 테스트용(Test) 데이터를 7:3 비율로 분할.

### 모델 학습 및 평가
다음 세 가지 모델을 사용하여 성능을 비교하였습니다.
1. **Random Forest**:
   - 초기 모델의 경우 전체 정확도(Accuracy)는 약 89%로 높았으나, 소수 클래스(가입자, Class 1)에 대한 재현율(Recall)이 약 24%로 낮아 불균형 데이터 문제를 확인했습니다.
   - `GridSearchCV`를 통해 하이퍼파라미터 튜닝(`n_estimators`, `max_depth`, `class_weight`)을 수행하여 성능 최적화를 시도했습니다.
2. **Logistic Regression**: 선형 모델을 통한 베이스라인 성능 확인.
3. **XGBoost**: 부스팅 알고리즘을 적용하여 예측 성능 비교.

### 모델 해석 (Interpretability)
- **Feature Importance**: 모델 예측에 중요한 변수 상위 10개를 추출하여 시각화하였습니다.
- **Partial Dependence Plot (PDP)**: 주요 변수(`poutcome`, `contact`, `age`, `balance` 등)가 예측 확률에 미치는 영향을 평균적으로 분석하였습니다.

### 최종 결론
- 데이터의 불균형(Imbalance)으로 인해 단순 정확도(Accuracy)보다는 **F1-Score** 및 **ROC-AUC**를 주요 평가지표로 활용해야 함을 확인했습니다.
- 다양한 모델(Random Forest, Logistic Regression, XGBoost)의 비교를 통해 최적의 예측 모델을 선정하는 과정을 거쳤습니다.
