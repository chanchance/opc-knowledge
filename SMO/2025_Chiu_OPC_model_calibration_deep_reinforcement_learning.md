# OPC Model Calibration Using Deep Reinforcement Learning

## 메타데이터
- **저자**: Weilun Chiu et al.
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV, 134251N (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3049598

## 핵심 요약
OPC(광학 근접 보정) 모델 보정(calibration)에 심층 강화 학습(deep reinforcement learning, DRL)을 적용하는 방법을 제시한다. OPC 모델 항(term)의 최적 조합을 찾고, 대응하는 파라미터에 대해 회귀(regression)를 수행하여 모델 예측 오차를 최소화하는 DRL 기반 자동 보정 프레임워크를 개발한다.

## 주요 기여
1. **DRL 기반 OPC 모델 보정**: 강화 학습으로 OPC 모델 항 선택 및 파라미터 최적화
2. **자동 모델 항 선택**: DRL 에이전트가 최적 OPC 모델 구성 요소 자동 탐색
3. **예측 오차 최소화**: 회귀 기반 파라미터 조정으로 모델 정확도 향상
4. **보정 자동화**: 전문가 경험 의존 없이 자동화된 OPC 모델 보정 달성

## 알고리즘/수식
### DRL 기반 OPC 모델 보정 프레임워크
```
강화 학습 설정:
  상태(State): 현재 OPC 모델 구성 (선택된 항 조합)
  행동(Action): 모델 항 추가/제거/파라미터 조정
  보상(Reward): -||CD_model - CD_measured||² (예측 오차 역수)

에이전트:
  Deep Q-Network (DQN) 또는 Policy Gradient
  입력: 현재 모델 상태 + 보정 데이터
  출력: 다음 최적 행동 (모델 항 선택)

OPC 모델 구조:
  모델 = Σ_k α_k · f_k(optical_image)
  여기서 f_k: k번째 모델 항 (resist, flare, M3D 등)
  α_k: DRL로 최적화된 가중치
```

### 모델 보정 최적화
```
최적화 목표:
  min_{항 선택, 파라미터} Σ_CD ||CD_sim - CD_meas||²

DRL 탐색 공간:
  - 광학 모델 항: sigma_in, sigma_out, 개구 형상 등
  - 레지스트 모델 항: diffusion, threshold, blur 등
  - EUV 특이 항: flare, M3D, stochastic

수렴:
  에피소드 반복으로 최적 모델 구성 수렴
  기존 수동 보정 대비 시간 단축
```

## OPC 툴 SMO 구현 관련성
- DRL OPC 모델 보정: SKOPC 모델 보정 모듈에서 DRL 기반 자동화 도입
- 모델 항 자동 선택: 전문가 없이 최적 OPC 모델 구성 자동 탐색
- SMO 최적화: DRL을 SMO 소스/마스크 공동 최적화에도 적용 가능
- EUV 모델 보정: EUV 특이 항(M3D, flare, stochastic) 자동 포함 여부 결정

## 태그
`OPC`, `model_calibration`, `deep_reinforcement_learning`, `DRL`, `machine_learning`, `EUV`, `automation`, `DTCO`, `SPIE`, `2025`
