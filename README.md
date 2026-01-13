# 💖 하트빌리지 : 이탈 원인 규명 및 유저 세그먼트별 그로스 전략
> **"DAU 90% 급감 문제 해결을 위한 AARRR 프레임워크 기반 데이터 진단 및 페르소나별 전략 제안"**

## 1. 프로젝트 개요 (Executive Summary)
* [cite_start]**배경**: 서비스 출시 초기 폭발적인 성장을 기록했으나, 특정 시점 이후 DAU가 약 **24.3K에서 2K 수준으로 급감**하며 서비스 유지의 위기 발생[cite: 55, 61].
* [cite_start]**목적**: 외부 여론(리뷰)과 내부 행동(로그) 데이터를 결합 분석하여 핵심 이탈 원인을 규명하고, 리텐션을 개선하기 위한 사용자 맞춤형 전략 수립[cite: 62].
* **핵심 성과**: 
    - [cite_start]**AARRR 퍼널 분석**을 통해 '투표 완료' 단계의 병목 구간 및 보상 체계의 불균형 확인[cite: 76].
    - [cite_start]**전체 전략 실행 시 이탈률 약 17%p 개선**(80.6% → 63.7%) 기대 수치 도출[cite: 108].

---

## 2. 분석 환경 (Analysis Environment)
* [cite_start]**사용 데이터**: 유저, 구매 기록, 투표 기록, 학급 등 **22개 테이블**로 구성된 서비스 로그 및 앱 리뷰 데이터[cite: 65].
* [cite_start]**기술 스택**: `Python`, `Scikit-Learn`, `XGBoost`, `SHAP`, `Tableau`[cite: 66, 207].

---

## 3. 분석 파이프라인 및 코드 구성 (Analysis Pipeline)

### 📂 [01-02] 데이터 전처리 및 EDA
* **파일**: `01_Preprocess.ipynb`, `02_Data_EDA.ipynb`
* **내용**: 22개 테이블 통합 및 시계열 지표 분석. [cite_start]서비스 고착도(Stickiness) 및 DAU 추이 분석을 통해 **2023년 6월 기점의 급격한 하락** 확인[cite: 130, 143].

### 📂 [03-04] 내부 데이터 분석 (Internal Analysis)
* **파일**: `03_AARRR_Analysis.ipynb`, `04_Stickness_Analysis.ipynb`
* [cite_start]**퍼널 진단**: '홈 화면 진입' 대비 '투표 완료' 전환율이 급격히 낮은 **Funnel Bottleneck** 구간 발견[cite: 76].
* [cite_start]**리텐션 특징**: 특정 업데이트 시점을 기준으로 리텐션이 급락하는 코호트 분석 결과 도출[cite: 76].


### 📂 [05] 외부 환경 분석 (External Analysis)
* **파일**: `05_Review_Analysis.ipynb`
* [cite_start]**리뷰 데이터**: Google Play Store 및 App Store 리뷰 **1,440건** 크롤링 및 LDA 토픽 모델링[cite: 70, 71].
* [cite_start]**핵심 인사이트**: 부정 리뷰의 70% 이상이 **'과도한 유료화', '광고 피로도', '시스템 오류'**에 집중되어 있으며, 정책 변화가 초기 충성 고객의 이탈을 가속화했음을 확인[cite: 72, 73].

### 📂 [06] ML 기반 이탈 요인 분석 (Churn Factor)
* **파일**: `06_Churn_Factor.ipynb`
* [cite_start]**주요 인자 도출**: 머신러닝(SHAP Value) 분석을 통해 이탈 예측의 핵심 변수로 **'출석 수(attendance_count)'**와 **'친구 수(friend_count)'**를 식별[cite: 150].


### 📂 [07] 유저 세그멘테이션 및 전략 (Segmentation)
* **파일**: `07_Segment_Persona_Strategy.ipynb`
* [cite_start]**활동성 점수(Activity Score) 정의**: 정량적 활동 지표를 단일화하여 유저 활동 지수 산출[cite: 83].
  [cite_start]$$ActivityScore = \beta_{1}(\text{Vote Count}) + \beta_{2}(\text{Social Share}) + \beta_{3}(\text{Login Freq})$$ [cite: 84]
* [cite_start]**사분위수(Quartile) 기반 분류**: 핵심 인자(출석, 친구 수) 기준 Q1~Q4 분류를 통해 **5대 세그먼트** 도출[cite: 81, 85].


---

## 4. 전략적 제언 및 기대효과 (Growth Strategy)

| 세그먼트 | 특징 | 전략 및 시뮬레이션 결과 |
| :--- | :--- | :--- |
| **Low-High** | 친구 많으나 접속 저조 | [cite_start]SNS 연계 바이럴 및 복귀 포인트 지급 → **이탈률 23.5%p 개선** 예상 [cite: 93, 96] |
| **High-Low** | 출석 높으나 친구 적음 | [cite_start]관심 친구 활동 실시간 PUSH 알림 전송 → **이탈 인원 692명 감소** 예상 [cite: 97, 100] |
| **전체 공통** | 지역 기반 랭킹 경쟁 | [cite_start]학교 대항 순위 경쟁 기능 도입 → **전체 이탈률 15.4%p 개선** 예상 [cite: 101, 106] |

---

## 5. 결론 및 회고 (Conclusion & Reflection)
* [cite_start]**결론**: AARRR 분석과 LDA 토픽 모델링을 통해 서비스 지표 급감 원인을 진단하고, 세그먼트별 맞춤형 그로스 전략 수립을 완료함[cite: 112].
* **회고 및 한계점**:
    - [cite_start]**검증 필요**: 사후 분석 기반 추론이므로 제안 전략의 실질적 효과 검증을 위한 **A/B Test** 설계 필요[cite: 114].
    - [cite_start]**데이터 기간**: 수집된 로그 기간이 짧아 장기적 리텐션 및 LTV(생애 가치) 파악에 제약 존재[cite: 115].
    - [cite_start]**공간 데이터**: 학교 위치 정보 부재로 지역 특성을 반영한 입지 최적화 분석까지 확장하지 못한 아쉬움[cite: 116].
