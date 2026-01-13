# 💖 Heart Village: 앱 서비스 문제 진단 및 그로스 전략 제안
> **"AARRR 및 NLP 분석을 통한 DAU 90% 급감 원인 규명 및 페르소나별 리텐션 전략 수립"**

## 1. Executive Summary
* **배경**: 하트빌리지 서비스는 초기 급격한 성장 이후, 특정 업데이트 시점을 기점으로 DAU가 약 **24.3K에서 2K 수준으로 90% 이상 급감**하는 위기 직면.
* **목적**: 로그 데이터(정량)와 앱 리뷰(정성)를 결합 분석하여 핵심 이탈 요인을 진단하고, 사용자 세그먼트별 맞춤형 그로스 전략을 제안함.
* **성과**: 
    - **AARRR 퍼널 분석**을 통해 '투표 완료' 단계의 병목 구간 및 보상 체계의 불균형 확인.
    - **활동지수(Activity Index)**를 설계하고 **중위수(Median)** 기준 교차 분류를 통해 4대 유저 페르소나 및 타겟팅 전략 도출.

---

## 2. Analysis Environment
* **Language**: `Python` (v3.9+)
* **Libraries**: 
    - **NLP**: `google-play-scraper`, `app-store-scraper`, `KoNLPy` (Okt)
    - **Data/ML**: `Pandas`, `NumPy`, `Scikit-learn`, `XGBoost`, `SHAP`, `Optuna`
    - **Visualization**: `Matplotlib`, `Seaborn`, `WordCloud`
* **Framework**: `AARRR Framework`, `LDA (Latent Dirichlet Allocation)`

---

## 3. Analysis Pipeline

### 📂 [01-02] Data Preprocessing & EDA
* 163만 건의 서비스 로그 및 외부 앱 리뷰 데이터 정제.
* 사용자 출석 빈도 및 서비스 지표 하락 추이 확인.

### 📂 [03-04] Service Diagnosis (AARRR & Stickiness)
* **AARRR Funnel**: '홈 화면 진입' 대비 '투표 완료' 전환율 분석을 통한 병목 구간 식별.
* **Stickiness**: DAU/MAU 지표 분석을 통해 서비스 고착도 급락 시점 및 이탈 패턴 정량화.


### 📂 [05-06] Churn Factor Analysis (NLP & ML)
* **NLP (External)**: 앱 리뷰 토픽 모델링(LDA) 결과, 부정적 여론의 핵심이 '과도한 유료화'와 '광고 피로도'임을 규명.
* **Churn Factor (Internal)**: XGBoost 및 SHAP을 활용하여 친구 수, 접속 간격 등 이탈에 기여하는 핵심 피처(Feature) 추출.


### 📂 [07] User Segmentation & Strategy
* **활동지수(Activity Index) 설계**: 유저의 서비스 관여도를 정량화하기 위해 가중치 기반 지표 산출.
  $$Activity\_Score = \beta_1(\text{Vote\_Count}) + \beta_2(\text{Social\_Share}) + \beta_3(\text{Interaction})$$
* **Median-based Cross-Segmentation**: 접속 빈도와 활동지수의 **중위수(Median)**를 기준으로 유저를 4개 페르소나로 그룹화.


---

## 4. Key Persona & Growth Strategy

| 페르소나 | 특징 | 그로스 전략 (Growth Strategy) |
| :--- | :--- | :--- |
| **Loyal (VIP)** | 접속/활동 모두 중위수 이상 | **오프라인 연계**: '아쿠' 캐릭터 굿즈 보상 및 학교 방문 이벤트로 소속감 강화 |
| **Potential** | 접속은 잦으나 활동성 낮음 | **참여 허들 완화**: 투표 리워드 강화 및 미션 수행형 보상 체계 도입 |
| **Reactive** | 접속은 낮으나 진입 시 활동적 | **리마인드 최적화**: 개인화된 푸시 알림을 통한 재방문 주기 단축 |
| **Inactive** | 모든 지표가 중위수 미만 | **Win-back**: 신규 기능 업데이트 및 복귀 유저 전용 프로모션 진행 |

---

## 5. Conclusion & Review

### **[결론]**
데이터 분석을 통해 서비스 급감의 원인이 기능적 결함보다는 '유료화 및 보상 정책'에 있음을 입증했습니다. 이를 해결하기 위해 유저를 세분화하고, 특히 고관여 유저를 위한 오프라인 경험(아쿠 캐릭터 굿즈 등)을 제안하여 리텐션 반등의 논리적 근거를 마련했습니다.

### **[한계점 및 향후 과제]**
* **데이터 기간의 한계**: 수집된 로그 데이터 기간이 짧아 장기적인 리텐션 추이 및 LTV(생애 가치) 산출에 제약이 있었습니다.
* **지리적 데이터 부재**: 학교 위치 등 상세 공간 데이터가 없어 지역별 특성을 반영한 입지 최적화 분석까지 확장하지 못한 아쉬움이 남습니다.
* **성과 검증**: 본 분석은 사후 데이터 기반의 전략 제안으로, 향후 실제 적용 시 **A/B Testing**을 통한 인과관계 검증이 필요합니다.
