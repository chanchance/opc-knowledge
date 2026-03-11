# Prediction of Etch Bias Using Random Forest Model

## 메타데이터
- **저자**: Wenrui Wang, Hua Shao, Rui Chen, Yayi Wei
- **연도**: 2024
- **게재지**: Proc. SPIE 12954, DTCO and Computational Patterning III, 129541F
- **DOI/URL**: https://doi.org/10.1117/12.3010574

## 핵심 요약
앙상블 학습 기반 Random Forest 알고리즘을 활용하여 에치 바이어스(etch bias)를 예측하는 모델을 개발한다. 1D 레이아웃에서 선폭(linewidth), 피치(pitch), 에치 바이어스 데이터를 학습 데이터로 사용하여 복잡한 에치 패턴 의존성을 포착한다.

## 주요 기여
1. Random Forest 앙상블 모델로 에치 바이어스 예측 문제 해결
2. 다수 결정 트리(decision tree) 조합으로 에치 공정의 비선형 패턴 의존성 포착
3. 선폭, 피치, 에치 바이어스 1D 레이아웃 데이터셋 구성 및 학습
4. 기존 룰 기반 또는 단순 회귀 모델 대비 예측 정확도 향상
5. OPC 흐름에 통합 가능한 빠르고 해석 가능한 에치 바이어스 예측기 제공

## 모델 수식/아키텍처
- **Random Forest**: N개 결정 트리의 앙상블
  - 각 트리: 입력 (linewidth, pitch, local_density) → 에치 바이어스 출력
  - 최종 예측: etch_bias = mean(tree_1, ..., tree_N)
- 특징 중요도(feature importance) 분석으로 에치 공정 물리 해석 가능
- 하이퍼파라미터: 트리 개수, 최대 깊이, 분할 기준(MSE/MAE)
- 교차 검증으로 과적합 방지 및 일반화 성능 평가

## 모델 유형
- [ ] 광학
- [ ] 레지스트
- [x] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC 에치 근접 보정 모듈에 Random Forest 에치 바이어스 예측기 통합 가능
- 학습 데이터 기반 에치 모델로 룰 기반 에치 테이블 대체 가능
- 특징 중요도 분석으로 에치 공정 핵심 파라미터 파악 → 공정 최적화에 활용
- 빠른 추론 속도로 풀칩 OPC 흐름에서 실시간 에치 바이어스 보정 적용 가능

## 태그
`Model`, `Etch`, `RandomForest`, `ML`, `EtchBias`, `OPC`, `EnsembleLearning`, `SPIE`, `DTCO`
