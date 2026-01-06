## 2025_1230

1. 프로젝트 개요
목표: 와인의 물리화학적 특성(산도, 당도, 알코올 등) 데이터를 기반으로 와인 품질 등급(0~10점)을 예측하는 머신러닝 모델 개발

데이터셋: UCI Red Wine Quality Dataset (샘플 수: 1,599개, 특성 수: 11개)

핵심 과제:

데이터 불균형(Class Imbalance): 전체 데이터의 약 82%가 5, 6점에 편중됨.

소수 클래스(3, 4, 8점)의 데이터 부족으로 인한 예측 성능 저하.

2. 분석 방법론 (Methodology)
본 프로젝트는 단계적 성능 개선 전략을 수립하여 수행하였다.

피처 엔지니어링 (Feature Engineering):

도메인 지식을 활용하여 모델의 변별력을 높이는 파생 변수 3종 생성.

주요 변수: alcohol_density (알코올과 밀도의 상호작용), so2_ratio (활성 이산화황 비율).

데이터 증강 (Data Resampling):

SMOTE (Synthetic Minority Over-sampling Technique) 기법 적용.

극소수 클래스(3, 4, 8점) 데이터를 합성하여 학습 데이터의 균형을 확보 (k_neighbors=1 설정).

모델 고도화 (Model Optimization):

단일 모델(Random Forest)의 한계를 극복하기 위해 Boosting 계열의 최신 알고리즘 도입.

XGBoost와 LightGBM을 결합한 Soft Voting Ensemble 모델 구축.

3. 주요 분석 결과 (Key Findings)
3.1. 정량적 성과
최종 앙상블 모델은 베이스라인 모델 대비 유의미한 성능 향상을 달성하였다.

정확도(Accuracy) 개선:

Random Forest (초기 모델): 64.38%

Ensemble (최종 모델): 67.50% (+3.12%p 상승)

계급별 재현율(Recall) 향상:

SMOTE 적용을 통해 기존에 예측이 불가능했던(Recall 0.00) 4점, 8점 등급의 탐지 능력 확보.

특히 데이터 비중이 높은 6점(Good) 등급의 예측 재현율을 **71%**까지 끌어올리며 전체 성능을 견인함.

3.2. 주요 영향 변수 (Feature Importance)
모델이 예측에 활용한 핵심 인자는 다음과 같으며, 이는 와인학(Enology)적 통념과 일치한다.

Alcohol (알코올) & Alcohol_density: 와인의 바디감과 품질을 결정하는 가장 강력한 양의 상관관계 변수로 확인됨.

Volatile Acidity (휘발성 산): 와인의 변질(식초 냄새)을 의미하며, 품질에 가장 큰 부정적 영향을 미치는 변수로 식별됨.

Sulphates (황산염): 와인의 산화 방지 및 보존성과 관련된 주요 인자로 확인됨.

4. 결론 및 제언 (Conclusion)
본 프로젝트는 불균형한 소규모 데이터셋이라는 한계 상황에서도 도메인 지식 기반의 피처 엔지니어링과 앙상블 기법을 통해 예측 한계치(SOTA 수준)에 근접한 67.50%의 정확도를 달성하였다.(Red wine 기준 작성)

5. 진짜 한줄평
-> GIGO

6. 확장
지역, 카테고리, 와이너리 기반 머신러닝










































###### Data url : [https://archive.ics.uci.edu/dataset/186/wine+quality]