# SRAF Printing Prediction Using Artificial Neural Network

## 메타데이터
- **저자**: Yonghwi Kwon, Jinho Yang, Sungho Kim, Cheolkyun Kim, Youngsoo Shin
- **연도**: 2020
- **게재지**: Proc. SPIE 11327, Optical Microlithography XXXIII, 113270C
- **DOI/URL**: https://doi.org/10.1117/12.2550685
- **인용수**: ~20

## 핵심 요약
SRAF(Sub-Resolution Assist Feature) 인쇄 가능성 검사(Printing Check)를 ANN(Artificial Neural Network)으로 빠르고 정확하게 수행하는 ML-SPC(Machine Learning-based SRAF Printing Check) 방법론을 제안한다. 기존 리소그래피 시뮬레이션 기반 SRAF 인쇄 검사는 정확하지만 시간이 많이 소요되는 반면, ANN 모델은 훈련 후 ms 단위의 빠른 추론으로 대용량 레이아웃의 SRAF 인쇄 여부를 즉시 예측한다.

## 주요 기여
1. ANN 기반 SRAF 인쇄 가능성 예측기(ML-SPC) 개발
2. 기존 리소그래피 시뮬 대비 수백~수천 배 빠른 SRAF 인쇄 검사
3. 공정 변동(Focus, Dose) 조건에서의 SRAF 인쇄 확률 예측
4. KAIST 연구팀의 고급 노드 검증

## Recipe/Process Flow 상세

### SRAF 인쇄 검사의 필요성과 도전
```
SRAF 삽입 흐름:
  1. SRAF 배치 (규칙 기반 또는 모델 기반)
  2. SRAF 인쇄 검사 (웨이퍼에 인쇄되면 결함!)
  3. OPC 적용
  4. 최종 검증

인쇄 검사 기존 방법:
  리소그래피 시뮬레이션:
    - 정확성: 높음
    - 속도: 느림 (SRAF 수천만 개 × 다중 공정 조건)
    - 전체 칩 적용 시 수십 시간 소요

ML-SPC 동기:
  - 훈련 후 추론: ms/SRAF → 전체 칩 수 분
  - 정확도: 시뮬레이션에 근접
  - 공정 변동 조건에서도 빠른 예측 가능
```

### ANN 기반 ML-SPC 모델
```
입력 피처 (SRAF별):
  SRAF 기하 특성:
    - SRAF 크기 (폭, 길이)
    - SRAF 방향 (수평/수직)
  주변 환경 특성:
    - 주 패턴 CD
    - 주 패턴-SRAF 거리 (inner space)
    - 인접 패턴 밀도
    - 피치
  공정 조건:
    - Focus (defocus 값)
    - Dose (노광 에너지)

출력:
  SRAF 인쇄 확률 P_print ∈ [0, 1]
  P_print > threshold → 인쇄 위험 (플래그)
  P_print < threshold → 안전 (인쇄 안 됨)

ANN 구조:
  입력층: N 피처 (수십 개)
  은닉층: 2-3 레이어, ReLU 활성화
  출력층: sigmoid (인쇄 확률)
  훈련: 이진 교차 엔트로피 손실
```

### 훈련 데이터 생성
```
데이터 수집:
  1. 다양한 SRAF 및 주변 패턴 조합 설계
  2. 리소그래피 시뮬로 SRAF 인쇄 여부 계산 (GT)
  3. (SRAF 피처, 인쇄 여부) 쌍 → 훈련 데이터

공정 변동 포함:
  (Focus, Dose) 그리드에서 시뮬레이션
  최악 조건(worst case)에서 인쇄 여부 결정
  또는 공정 조건을 피처에 포함

불균형 처리:
  대부분의 SRAF: 인쇄 안 됨 (비율 불균형)
  오버샘플링 또는 클래스 가중치로 처리
```

### ML-SPC 통합 SRAF 흐름
```
전통 SRAF 삽입 흐름:
  레이아웃 → SRAF 배치 → 리소그래피 시뮬(느림) → 인쇄 제거 → OPC

ML-SPC 통합 흐름:
  레이아웃 → SRAF 배치 → ML-SPC(빠름) → 인쇄 위험 SRAF 제거/축소 → OPC
  확인 단계: ML-SPC 결과 일부 리소그래피 시뮬로 검증

SRAF 크기 자동 조정 루프:
  While 인쇄 위험 SRAF 존재:
    SRAF 크기 축소 → ML-SPC 재평가 → 안전하면 완료
  → 안전한 최대 크기 SRAF 자동 결정
```

### 성능 결과 (KAIST + 선진 노드)
```
예측 정확도:
  AUC (Area Under ROC Curve): 0.95 이상
  인쇄 위험 SRAF 감지율: 높음 (>95%)
  False positive: 낮음 (과도한 SRAF 제거 방지)

런타임 비교:
  리소그래피 시뮬: 기준 (100%)
  ML-SPC: 수백~수천 배 빠름 (수 ms/SRAF)
  전체 칩 SRAF 검사: 수십 시간 → 수 분

공정 변동 조건:
  Focus/Dose 변동에 따른 인쇄 확률 예측 가능
  최악 조건 SRAF 크기 마진 자동 계산
```

## OPC 툴 구현 관련성
- **SKOPC SRAF 인쇄 검사**: `skopc/modeling/sraf_generator.py`에 ML-SPC 추론 모듈 추가
- **ANN 모델 서빙**: scikit-learn MLP 또는 PyTorch 모델로 SRAF 인쇄 확률 즉시 예측
- **SRAF 크기 자동화**: ML-SPC 피드백으로 SRAF 크기를 안전 범위 내 최대로 자동 설정
- **전체 칩 적용**: `skopc/recipe/` 배치 처리에서 SRAF 삽입 후 ML-SPC 일괄 실행

## 참고문헌
- Proc. SPIE 11327, Optical Microlithography XXXIII (2020)
- 저자 소속: KAIST (Korea Advanced Institute of Science and Technology)
- 관련: Process optimization through model-based SRAF printing prediction (SPIE 8326, 2012)
- 관련: SRAF printing prediction using logistic regression (SPIE 9426, 2015)
- 관련: Full-chip ML SRAFs on DRAM case (SPIE 10961, 2019)

## 태그
`Recipe`, `SPIE`, `SRAF`, `PrintingPrediction`, `ArtificialNeuralNetwork`, `ML-SPC`, `MachineLearning`, `ProcessWindow`, `KAIST`, `2020`
