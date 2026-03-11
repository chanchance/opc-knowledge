# Co-optimization of Optical and Resist Models in the OPC Modeling Process Using In-House Genetic Algorithm

## 메타데이터
- **저자**: Yinuo Pan, Yingfang Wang, Norman Chen, Keeho Kim, Eric Parent
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II
- **DOI/URL**: https://doi.org/10.1117/12.2657959

## 핵심 요약
기존의 광학 모델과 레지스트 모델을 순차적으로 최적화하는 방식 대신, 자체 개발 유전 알고리즘(GA)으로 두 모델을 동시에 공동 최적화한다. 파레토 최적 프런티어를 탐색하여 더 나은 해 후보를 찾고, 알고리즘이 국소 최적해에 갇힐 때 탐색 범위를 확대하는 방법을 제안한다.

## 주요 기여
1. 광학 모델 + 레지스트 모델의 동시 공동 최적화 방법론 제안
2. 파레토 최적 프런티어 탐색으로 두 모델 간 균형 잡힌 최적해 도출
3. 자체 개발 GA로 국소 최적해 탈출 전략 구현 (탐색 범위 동적 확대)
4. 순차 최적화 대비 전체 OPC 모델 예측 정확도 향상
5. OPC 모델 교정 자동화 파이프라인에서의 GA 실용성 검증

## 모델 수식/아키텍처
- **공동 최적화 문제**:
  - 목적 함수 1: min RMSE_optical (광학 모델 예측 오차)
  - 목적 함수 2: min RMSE_resist (레지스트 모델 예측 오차)
  - 파레토 최적: (θ_optical, θ_resist) 쌍의 파레토 프런티어 탐색
- **GA 구현**:
  - 염색체: 광학 파라미터 (커널 계수) + 레지스트 파라미터 (σ, n, t_r) 결합
  - 적합도: 가중 합산 RMSE 또는 파레토 지배 기반 순위
  - 탐색 범위 확대: 수렴 정체 감지 시 돌연변이율 증가
- 교정 데이터: ArF/EUV 게이지 패턴의 CD 측정값

## 모델 유형
- [x] 광학
- [x] 레지스트
- [x] ML/DL (메타휴리스틱 공동 최적화)
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC 모델 교정 파이프라인에서 광학-레지스트 공동 최적화 구현 참조
- `2005_Huang_OPCModel_GeneticAlgorithm.md`의 GA 방법론을 공동 최적화로 확장
- `2025_Chiu_DRL_OPCModelCalibration.md`와 함께 자동화 모델 교정 최적화 기술 비교
- 파레토 다목적 최적화로 OPC 모델 교정의 트레이드오프 관리

## 태그
`Model`, `Calibration`, `GeneticAlgorithm`, `CoOptimization`, `Pareto`, `OPC`, `OpticalModel`, `ResistModel`, `SPIE`, `DTCO`
