# OPC Model Calibration Using Deep Reinforcement Learning

## 메타데이터
- **저자**: Weilun Chiu, Tony Hu, Terry Hsuan, Elvis Yang, T. H. Yang, K. C. Chen
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134251N
- **DOI/URL**: https://doi.org/10.1117/12.3049598
- **인용수**: 신규 논문 (SPIE Advanced Lithography 2025)

## 핵심 요약
OPC 모델 캘리브레이션은 모델 용어의 최적 조합을 찾고 파라미터 회귀를 수행하여 모델 예측 오차를 최소화하는 것이 목표다. 딥러닝이 계산 리소그래피에서 우수한 결과를 달성한 것에서 착안하여, 심층 강화학습(Deep RL)을 적용한 에이전트(Agent)를 훈련하여 OPC 모델 파라미터를 예측한다. 보상 함수는 OPC 모델 캘리브레이션의 RMSE 음수값으로 정의하며, VIA 레이어 실험에서 기존 순차적 캘리브레이션 방법과 동등한 성능을 달성한다.

## 주요 기여
1. OPC 모델 파라미터 최적화에 Deep RL(Actor-Critic) 적용 — 전통적 순차적 최적화 대체
2. 두 가지 접근법:
   - 직접 예측: RL 모델이 모든 OPC 파라미터를 직접 예측
   - 차원 축소: VAE/PCA/Kernel PCA로 OPC 파라미터를 4차원으로 압축 후 RL 적용
3. VIA 레이어에서 기존 순차 캘리브레이션 대비 동등한 정확도 달성 실증
4. 캘리브레이션 복잡도와 시간 저감 가능성 제시

## 검증 방법론
- **Deep RL 프레임워크**:
  - Agent: OPC 모델 파라미터를 예측하는 정책 신경망
  - 환경: OPC 모델 캘리브레이션 엔진
  - 보상: `-RMSE(캘리브레이션 오차)` — 오차 최소화 = 보상 최대화
- **차원 축소 접근법**:
  - VAE(Variational Autoencoder): OPC 파라미터 공간을 잠재 벡터(4차원)로 압축
  - PCA/Kernel PCA: 선형/비선형 차원 축소
  - RL Agent가 잠재 공간에서 탐색 → 원래 파라미터 공간으로 디코딩
- **평가 지표**:
  - 캘리브레이션 RMSE: RL 방법 vs. 기존 순차 최적화 비교
  - 파라미터 수렴 이터레이션 수
  - VIA 레이어 CD 예측 정확도

## 검증 지표
- EPE 허용 범위: VIA 레이어 OPC 모델 RMSE (기존 방법 대비 동등 수준)
- 시뮬레이터: OPC 모델 캘리브레이션 엔진 (컴팩트 광학+레지스트 모델)
- 커버리지: VIA 레이어 다양한 CD/피치 조합

## OPC 툴 구현 관련성
- **OPC 모델 자동 캘리브레이션 모듈 고도화**: `ModelingEngine`의 OPC 모델 파라미터 최적화 루프에 RL 기반 파라미터 탐색을 통합하는 설계 근거
- VAE 기반 OPC 파라미터 공간 압축은 고차원 모델 파라미터 탐색 효율을 대폭 향상시키는 구현 방법
- 보상 함수 정의(`-RMSE`)는 OPC 모델 캘리브레이션 목적 함수를 RL 최적화 문제로 재구성하는 방법론 제공
- 기존 순차 캘리브레이션과 동등한 정확도를 달성하므로 기존 플로우 대체 가능성 입증

## 참고문헌
- SPIE DTCO and Computational Patterning IV 2025, Vol. 13425
- OPC 모델 캘리브레이션 관련 선행 연구 (MB-OPC RL 적용 연구들)

## 태그
`Verification`, `SPIE`, `OPCModel`, `Calibration`, `DeepReinforcementLearning`, `VAE`, `PCA`, `ParameterOptimization`, `VIA`, `RMSE`
