# OPC Model Calibration Using Deep Reinforcement Learning

## 메타데이터
- **저자**: Chiu, W., Hu, T., Hsuan, T., Yang, E., Yang, T.H., Chen, K.C.
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV
- **DOI/URL**: https://doi.org/10.1117/12.3049598
- **인용수**: ~3

## 핵심 요약
OPC 모델 파라미터 최적 조합을 탐색하는 캘리브레이션 문제에 심층 강화학습(DRL)을 적용한다. 에이전트(Agent)가 OPC 모델 파라미터를 예측하고, 보상 함수로 캘리브레이션 RMS 오차의 음수를 사용하여 최소 예측 오차를 달성하도록 학습한다. VAE/PCA로 파라미터 공간을 압축하는 차원 축소 접근법도 제안하며, VIA 레이어에서 기존 순차 캘리브레이션과 동등한 성능을 실증한다.

## 주요 기여
1. OPC 모델 캘리브레이션에 DRL 최초 체계적 적용
2. 직접 파라미터 예측 방식: DRL 에이전트가 전체 OPC 파라미터 벡터 직접 출력
3. 차원 축소 방식: VAE/PCA로 파라미터 공간 4D로 압축 후 DRL 탐색
4. 기존 GA·Simulated Annealing·Gradient Descent 대비 탐색 효율성 비교
5. VIA 레이어 실험: 기존 순차 캘리브레이션과 동등한 RMS 달성

## 모델 수식/아키텍처

**강화학습 프레임워크:**
```
State s_t: 현재 파라미터 추정값 θ_t + 캘리브레이션 오차 통계
Action a_t: Δθ (파라미터 업데이트 방향/크기)
Reward r_t: -RMS(θ_t + a_t)  [RMS 감소 = 양의 보상]
```

**DRL 에이전트 (Actor-Critic):**
```
Actor π(a|s; φ): state → action 확률분포 (파라미터 업데이트 제안)
Critic V(s; ψ): state → value 추정
업데이트: PPO (Proximal Policy Optimization) 또는 SAC
```

**차원 축소 접근법:**
```
VAE 인코더: θ (고차원) → z (4D latent)
DRL 탐색: z 공간에서 최적 z* 탐색
VAE 디코더: z* → θ* (최적 파라미터 복원)
```

**보상 함수:**
```
r = -RMS(θ) = -sqrt(1/N · Σ_i (CD_sim(θ,i) - CD_meas,i)²)
```

**탐색 효율 비교:**
```
Gradient Descent: 국소 최적해 위험, 빠름
GA: 전역 탐색, 느림 (O(P·G) 평가)
DRL: 경험 기반 효율적 탐색, 학습 후 빠름
DRL+VAE: 저차원 탐색으로 더욱 효율적
```

## 모델 유형
- [ ] 광학 모델
- [ ] 레지스트 모델
- [x] ML/DL (심층 강화학습)
- [x] 하이브리드 (DRL + 물리 OPC 모델 캘리브레이션)

## OPC 툴 구현 관련성
- skopc 캘리브레이션 엔진에 DRL 옵션 추가 (GA 대안으로)
- 사전 학습된 DRL 에이전트: 새 레이어/공정에 소량 파인튜닝으로 재사용
- VAE 차원 축소: 파라미터 공간이 수십~수백 차원인 경우 특히 유효
- DRL 탐색 환경: OPC 모델 평가 함수를 환경으로 래핑
- 기존 방법 대비 우위: 이전 탐색 경험 활용 → 반복 캘리브레이션 효율화

## 참고문헌
- Huang, Y.-H. et al., "Effective OPC model calibration using ML" (2022)
- Lee, S. et al., "Co-optimization of optical and resist models with GA" (2023)
- Schulman, J. et al., "Proximal Policy Optimization" (2017, arXiv)

## 태그
`Model`, `SPIE`, `DeepReinforcementLearning`, `OPCCalibration`, `VAE`, `PCA`, `DRL`, `2025`
