# Model-Based OPC With Adaptive PID Control Through Reinforcement Learning

## 메타데이터
- **저자**: (IEEE Xplore document 10847731 - 상세 저자 정보 추가 확인 필요)
- **연도**: 2025
- **게재지**: IEEE Transactions on Semiconductor Manufacturing (추정)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10847731/
- **인용수**: 신규 논문

## 핵심 요약
Model-based OPC(MB-OPC)는 EPE를 기반으로 한 피드백 루프에 의존하는데, 이 루프의 PID 제어 파라미터 튜닝이 수렴 속도와 정확도에 결정적 영향을 미친다. 본 논문은 강화학습(RL)을 통해 PID 게인을 적응적으로 조정하는 방법론을 제안하여, 다양한 패턴 유형과 공정 조건에서 OPC 수렴을 자동 최적화한다.

## 주요 기여
1. RL 기반 PID 게인 자동 적응 메커니즘 — 패턴 유형별 최적 PID 파라미터 학습
2. MB-OPC 피드백 루프를 Markov Decision Process(MDP)로 정형화
3. 다양한 레이아웃 구조에서 수렴 속도 및 EPE 정확도 동시 향상
4. 전통적 PID 튜닝의 수동 노력 제거

## Recipe/Process Flow 상세

### MB-OPC 피드백 루프 재정의 (MDP)
```
상태(State): 현재 이터레이션의 EPE 분포, 패턴 문맥 정보
행동(Action): PID 게인 조정 (ΔKp, ΔKi, ΔKd)
보상(Reward): EPE 감소량 - 이터레이션 비용 × 패널티

에피소드: 하나의 OPC 레시피 실행 (초기 마스크 → 수렴까지)
```

### 적응형 PID OPC 알고리즘
```
For each OPC iteration k:
  1. 리소그래피 시뮬레이션 실행
  2. EPE 측정: e(k) = target_CD - simulated_CD
  3. RL 에이전트로부터 PID 게인 획득:
     [Kp(k), Ki(k), Kd(k)] = RL_agent(state(k))
  4. 세그먼트 이동량 계산:
     u(k) = Kp(k)·e(k) + Ki(k)·Σe(j) + Kd(k)·[e(k)-e(k-1)]
  5. 마스크 업데이트
  6. 수렴 체크: RMS_EPE < threshold → 종료
  7. RL 에이전트 업데이트 (보상 기반)
```

### RL 학습 구성
- **정책 네트워크**: LSTM 또는 MLP (EPE 시계열 처리)
- **학습 알고리즘**: PPO(Proximal Policy Optimization) 또는 SAC
- **훈련 데이터**: 다양한 패턴 유형의 OPC 시뮬레이션 데이터
- **적응 능력**: 신규 패턴 유형에 대해 온라인 적응 가능

### 수렴 개선 결과
- 기존 고정 PID 대비 이터레이션 수 감소
- EPE 수렴 정확도 향상
- 다양한 공정 조건 변화에 강건한 수렴

## OPC 툴 구현 관련성
- **SKOPC Model OPC**: `skopc/modeling/model_opc.py` 수렴 루프에 RL 기반 적응형 게인 제어 통합 가능
- **2004년 논문 확장**: Painter et al.(2004) PID 제어 이론을 RL로 자동화한 최신 발전
- **실용성**: 레시피 엔지니어가 PID 게인을 수동 튜닝하는 작업 제거
- **GNN-OPC 시너지**: `skopc/modeling/gnn/`의 초기 보정 예측과 조합 가능

## 참고문헌
- IEEE Xplore Document 10847731 (2025)
- 관련: Classical control theory applied to OPC correction segment convergence (SPIE, 2004)
- 관련: Design of automatic controllers for model-based OPC (SPIE, 2008)

## 태그
`Recipe`, `IEEE`, `ModelBasedOPC`, `PID-Control`, `ReinforcementLearning`, `AdaptiveControl`, `Convergence`, `EPE`, `2025`
