# Budgeting and Predicting Pattern Defects Using Edge Placement Error and Machine Learning

## 메타데이터
- **저자**: Sandip Halder et al.
- **연도**: 2023
- **게재지**: IEEE Conference Publication, IEEE Xplore 10102957
- **DOI/URL**: https://ieeexplore.ieee.org/document/10102957/
- **인용수**: 신규 논문

## 핵심 요약
EPE(Edge Placement Error)를 극값 통계(extreme value statistics) 기반 지표로 활용하여 CD 도메인과 오버레이 도메인의 모든 변동을 결합한다. 이 EPE 지표를 통해 공정 성능을 특성화하고, 최종적으로 수율을 모니터링하는 ML 기반 패턴 결함 예측·예산 배분(budgeting) 방법론을 제시한다.

## 주요 기여
1. EPE를 극값 통계로 정의하여 CD+오버레이 결합 변동을 단일 지표로 정량화하는 프레임워크 확립
2. ML 기반 패턴 결함 예측 모델 — EPE 입력으로부터 결함 확률 예측
3. EPE 예산 배분(Budget Allocation) 방법론 — 레이어·공정 단계별 EPE 허용량 최적 배분
4. 공정 성능 모니터링과 수율 예측을 EPE 단일 지표로 통합하는 실용적 플로우

## 검증 방법론
- **EPE 극값 통계 프레임워크**:
  - EPE를 GEV(Generalized Extreme Value) 분포로 모델링
  - Tail 분포의 특성화로 저확률 고위험 결함(rare defect) 예측
- **ML 패턴 결함 예측**:
  - 입력: EPE 통계 파라미터 (평균, 표준편차, tail 지수)
  - 출력: 패턴 결함 발생 확률
  - 모델: 앙상블 또는 신경망 기반 회귀/분류
- **EPE 예산 배분**: 각 EPE 기여 요인(OPC 오차, 오버레이, stochastic 등)의 허용 기준을 수율 목표에 맞게 최적화
- **검증**: 실제 공정 데이터로 예측 결함 확률과 실측 결함 밀도 상관관계 검증

## 검증 지표
- EPE 허용 범위: 극값 통계 기반 — 결함 확률 < 목표값 (예: 10⁻⁴/패턴)이 되는 EPE 한계
- 시뮬레이터: ML 예측 모델 (극값 통계 입력 기반)
- 커버리지: CD + 오버레이 도메인 전체 변동 통합 분석

## OPC 툴 구현 관련성
- **OPC 검증에서 결함 확률 기반 EPE 기준 설정**: 단순 EPE 임계값 대신 결함 확률로 검증 기준을 정의하는 방법론 — `VerificationEngine`의 EPE 판단 로직을 통계 기반으로 고도화하는 설계 근거
- EPE 예산 배분 알고리즘으로 OPC 잔류 EPE 허용량을 시스템 수준에서 결정하는 프레임워크 제공
- 극값 통계 기반 결함 확률 계산은 EUV 스토캐스틱 OPC 검증에 직접 적용 가능
- 공정 모니터링과 OPC 검증 결과를 연계한 수율 예측 모듈 구현의 이론적 기반

## 참고문헌
- IEEE Conference 2023 (IITC 또는 관련 반도체 공정 컨퍼런스)
- EPE 극값 통계 관련 선행 연구들

## 태그
`Verification`, `IEEE`, `EPE`, `ExtremeValueStatistics`, `MachineLearning`, `PatternDefect`, `YieldPrediction`, `EPEBudget`, `Stochastic`, `EUV`
