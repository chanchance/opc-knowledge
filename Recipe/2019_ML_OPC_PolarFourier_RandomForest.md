# Optimization of Machine Learning Guided Optical Proximity Correction

## 메타데이터
- **저자**: (IEEE document 8623985 - 2019 IEEE Conference)
- **연도**: 2019
- **게재지**: IEEE Conference Publication (ICCAD 또는 DAC 계열)
- **DOI/URL**: https://ieeexplore.ieee.org/abstract/document/8623985
- **인용수**: ~40

## 핵심 요약
ML 기반 OPC(ML-OPC)에서 레이아웃 세그먼트 표현과 회귀/분류기 선택이 핵심임을 분석하고, 극 푸리에 변환(Polar Fourier Transform, PFT) 신호와 초기 EPE를 세그먼트 표현으로, 랜덤 포레스트 회귀기(Random Forest Regressor, RFR)를 ML 알고리즘으로 제안한다. 최신 ML-OPC 대비 마스크 바이어스 예측의 RMS 오차를 1.45nm에서 0.66nm로 55% 감소시킨다.

## 주요 기여
1. PFT(Polar Fourier Transform) 기반 세그먼트 표현 — 회전 불변성과 압축적 표현
2. 초기 EPE를 추가 피처로 활용하여 문맥 정보 강화
3. RFR(Random Forest Regressor) — OPC 마스크 바이어스 예측에 최적화
4. 최신 ML-OPC 대비 RMS 오차 55% 감소 (1.45nm → 0.66nm)

## Recipe/Process Flow 상세

### PFT 기반 세그먼트 표현
```
기존 ML-OPC 세그먼트 표현:
  - 주변 패턴의 직교 좌표 마스크 이미지
  - 한계: 회전/반전에 민감, 고차원

PFT(Polar Fourier Transform) 표현:
  1. 세그먼트 중심 기준 극좌표(r, θ)로 변환
  2. 극좌표 도메인에서 2D Fourier 변환
  3. 주파수 스펙트럼 추출 (저주파 계수만 사용)

장점:
  - 회전 불변성: 회전된 동일 패턴 → 유사한 PFT 계수
  - 압축적 표현: 낮은 차원으로 풍부한 정보 포함
  - 물리적 의미: 주파수 계수가 광학 회절 특성 반영
```

### 초기 EPE 피처 통합
```
기존 방식:
  입력: 레이아웃 기하학 피처 → 마스크 바이어스 예측

개선 방식:
  입력: [레이아웃 PFT 피처 | 초기 EPE]
        → 마스크 바이어스 예측

초기 EPE 역할:
  - 명목 조건(best focus, best dose)에서의 오차 정보
  - 어느 방향으로 얼마나 보정할지 힌트 제공
  - 비선형 효과 (MEEF 등) 포착에 도움
```

### Random Forest Regressor 적용
```
RFR 선택 이유:
  1. 비모수적 방법: OPC 비선형 관계 포착
  2. 앙상블: 과적합 방지, 분산 감소
  3. 피처 중요도: OPC 물리 이해 가능
  4. 빠른 훈련/추론: 실용적 속도

RFR 구성:
  - 트리 수: N (일반적으로 100-500)
  - 최대 깊이: 과적합 방지 하이퍼파라미터
  - 피처 서브샘플링: 각 분기에서 무작위 피처 선택
  - 최종 예측: N 트리 예측의 평균
```

### ML-OPC 통합 흐름
```
훈련 단계:
  기존 OPC 결과 → (레이아웃 PFT + 초기 EPE, 최적 바이어스) 쌍
  → RFR 훈련

추론 단계 (OPC 가속):
  새 레이아웃 → PFT 추출 → 초기 EPE 계산
              → RFR 예측 → 초기 마스크 바이어스
              → 표준 OPC (소수 이터레이션)
```

### 성능 결과
```
마스크 바이어스 예측 RMS 오차:
  기존 ML-OPC: 1.45 nm
  본 방법 (PFT + RFR): 0.66 nm
  개선: 55% 감소

이터레이션 수: 초기 바이어스 개선으로 감소
런타임: ML 추론 속도
```

## OPC 툴 구현 관련성
- **SKOPC GNN-OPC 대안**: `skopc/modeling/gnn/` GNN 대신 PFT+RFR 기반 바이어스 예측기 구현 가능
- **PFT 피처 추출**: 극좌표 기반 세그먼트 표현은 회전 등변성 문제 해결에 효과적
- **RFR**: scikit-learn RandomForestRegressor로 간단히 구현 가능
- **초기 EPE**: `skopc/core/litho_engine.py`에서 명목 조건 EPE 계산 후 ML 입력으로 활용

## 참고문헌
- IEEE Conference Publication 2019, Document 8623985
- 관련: Neural Network Classifier-Based OPC (IEEE TCAD, 2018)
- 관련: Intelligent model-based OPC (SPIE 6154, 2006)
- 관련: Efficient Model-Based OPC via GNN (IEEE ISEDA 2023)

## 태그
`Recipe`, `IEEE`, `ML-OPC`, `PolarFourier`, `RandomForest`, `MachineLearning`, `MaskBias`, `EPE`, `FeatureRepresentation`, `2019`
