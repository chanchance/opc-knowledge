# OPC Model Calibration Using Deep Reinforcement Learning

## 메타데이터
- **저자**: Weilun Chiu, Tony Hu, Terry Hsuan, Elvis Yang, T.H. Yang, K.C. Chen
- **연도**: 2025
- **게재지/학회**: SPIE Advanced Lithography + Patterning, Proc. SPIE 13425, DTCO and Computational Patterning IV
- **DOI/URL**: https://doi.org/10.1117/12.3049598; https://www.spiedigitallibrary.org/conference-proceedings-of-spie/13425/134251N/
- **인용수**: 신규 (2025년)

## 핵심 요약
심층 강화 학습(DRL: Deep Reinforcement Learning)을 OPC 모델 보정(calibration) 파라미터 자동 탐색에 적용한 논문. OPC 모델 보정은 모델 항(term)의 최적 조합과 해당 파라미터 회귀를 통해 예측 오차를 최소화하는 과정으로, 전통적으로는 인간 전문가의 반복적 조정이 필요하다. DRL 에이전트(Agent)가 보상 함수(OPC 모델 교정 RMSE의 음수)를 통해 자동으로 파라미터를 예측하며, VAE(변분 자동인코더) 또는 PCA를 이용한 파라미터 차원 축소 방법도 함께 제안한다. VIA 레이어 실험에서 기존 순차적 보정 방법과 동등한 성능을 달성하여 OPC 파라미터 최적화의 실용적 대안임을 입증한다.

## 주요 기여
- DRL(Deep Reinforcement Learning)을 OPC 모델 보정에 최초 적용
- 보상 함수 설계: 교정 RMSE의 음수 → 파라미터 품질 신호
- 두 가지 접근법: 직접 예측 vs. 차원 축소 후 예측
- VAE/PCA 기반 OPC 파라미터 차원 축소로 탐색 공간 축소
- 기존 순차적 보정 방법과 동등한 성능 + 반복 시간 감소 가능성

## 모델 아키텍처/수식
**OPC 모델 파라미터 보정 문제:**
```
Objective: min_{θ_OPC} RMSE(θ_OPC)
         = min_{θ_OPC} √(Σᵢ (CD_sim(θ_OPC, pattern_i) - CD_meas,i)² / N)
```
θ_OPC: OPC 모델 파라미터 벡터 (수십 ~ 수백 개)
고차원 비선형 최적화 문제

**DRL 기반 보정 프레임워크:**

State: 현재 모델 파라미터 상태 + 보정 패턴 특성
```
s_t = (θ_OPC,t, gauge_features)
```

Action: 파라미터 조정량
```
a_t = Δθ_OPC   (연속 행동 공간)
```

Reward: 보정 품질
```
r_t = -RMSE(θ_OPC,t + a_t)   (낮은 RMSE → 높은 보상)
```

Policy Network (Actor-Critic 기반):
```
π_θ(a_t | s_t): 행동 확률 분포
V_φ(s_t): 상태 가치 추정
```

**방법 1: 직접 예측**
```
θ_OPC = π_θ(gauge_features)   (DRL 에이전트가 직접 파라미터 예측)
```

**방법 2: 차원 축소 후 예측**
VAE 기반 차원 축소:
```
θ_OPC → Encoder → z (4차원 잠재 벡터)
z → Decoder → θ̂_OPC
z = μ(θ_OPC) + ε·σ(θ_OPC)   (reparameterization)
```

DRL이 잠재 공간에서 탐색:
```
z* = DRL_agent(gauge_features)
θ_OPC* = Decoder(z*)
```

PCA 대안:
```
z = PCA_transform(θ_OPC, n_components=4)
θ_OPC = PCA_inverse(z)
```

**학습 알고리즘: PPO (Proximal Policy Optimization)**
```
L_PPO = E[min(r_t(θ)·Â_t, clip(r_t(θ), 1-ε, 1+ε)·Â_t)]
r_t(θ) = π_θ(a_t|s_t) / π_θ_old(a_t|s_t)
Â_t: 이점(advantage) 추정치
```

**VIA 레이어 실험 결과:**
- RMSE: 기존 순차적 보정 대비 동등 수준
- 반복 횟수: 잠재적으로 감소
- 자동화 정도: 인간 개입 최소화

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [ ] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 모델 보정 자동화 방향에 중요한 참조. 현재 SKOPC에서 수동으로 조정하는 OPC 모델 파라미터를 DRL로 자동 최적화하는 방향으로 발전 가능. `skopc/modeling/` 내 calibration 루틴에 PPO 기반 파라미터 탐색 기능 추가 시 이 논문의 reward 함수 설계와 VAE 기반 파라미터 압축 방법 참조. VIA 레이어에서 검증되었으므로 SKOPC의 `recipes/example_arfimm.yaml` via 레이어 보정에 적용 가능.

## 참고문헌 (핵심)
- Schulman, J. et al., "Proximal policy optimization algorithms (PPO)," arXiv:1707.06347 (2017)
- Kingma, D.P. and Welling, M., "Auto-encoding variational Bayes (VAE)," ICLR 2014
- Mnih, V. et al., "Human-level control through deep reinforcement learning (DQN)," Nature (2015)
- Sturtevant, J. and Tejnil, E., "Roadmap to sub-nanometer OPC model accuracy," SPIE 8441 (2012)

## 태그
`Model`, `OPC`, `Calibration`, `ReinforcementLearning`, `DRL`, `PPO`, `VAE`, `PCA`, `AutomaticCalibration`, `SPIE`, `VIA`, `ParameterOptimization`, `2025`
