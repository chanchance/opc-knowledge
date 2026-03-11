# Model-Based OPC With Adaptive PID Control Through Reinforcement Learning

## 메타데이터
- **저자**: Taeyoung Kim, Shilong Zhang, Youngsoo Shin
- **연도**: 2025
- **게재지**: IEEE Transactions on Semiconductor Manufacturing
- **DOI/URL**: https://ieeexplore.ieee.org/document/10847731/
- **인용수**: 신규 논문

## 핵심 요약
모델 기반 OPC(MB-OPC)는 EPE를 보정 결과 측정 지표로 사용하는 피드백 루프에 의존하며, PID 제어가 이 피드백 루프에서 일반적으로 사용된다. 기존 MB-OPC는 P 제어만 활용하는 한계가 있다. 본 논문은 강화학습(RL)을 적용하여 보정 루프 내에서 PID 계수를 적응적으로 산출하는 훈련된 actor를 구성한다. Supervised pre-training으로 초기 가중치를 신속히 설정하고, critic이 정확한 Q-value(누적 보상)를 예측하도록 훈련된다.

## 주요 기여
1. RL 기반 적응형 PID 제어를 MB-OPC 보정 루프에 통합 — P 제어만 사용하는 기존 한계 극복
2. Actor-Critic RL 구조로 OPC 수렴 속도 및 EPE 최소화 성능 향상
3. Supervised pre-training으로 RL 초기 수렴 안정성 확보 — 훈련 효율 개선
4. OPC 보정 루프를 제어 이론(PID) + ML(RL)의 하이브리드로 재해석한 새로운 프레임워크

## 검증 방법론
- **MB-OPC 피드백 루프**: 각 이터레이션에서 시뮬레이션 컨투어의 EPE를 계산하고 PID 제어로 엣지 이동량 결정
- **RL Actor**: 현재 EPE 상태를 입력받아 최적 PID 계수(Kp, Ki, Kd)를 출력
- **RL Critic**: 예상 누적 보상(Q-value)을 추정하여 Actor 학습을 가이드
- **Supervised Pre-training**: 표준 MB-OPC의 동작을 모방하여 Actor 초기 가중치 신속 설정
- **평가 지표**:
  - OPC 수렴 이터레이션 수 (기존 P 제어 대비 감소)
  - 최종 EPE 분포 (평균, 표준편차, 최대값)
  - 보정 후 EPE 잔류량 (residual EPE)

## 검증 지표
- EPE 허용 범위: 선단 노드 OPC 기준 (수 nm 이내 잔류 EPE)
- 시뮬레이터: 컴팩트 리소그래피 모델 기반 MB-OPC 엔진
- 커버리지: 다양한 패턴 유형 (라인/스페이스, 콘택트, 2D 패턴)

## OPC 툴 구현 관련성
- **OPC 보정 루프 알고리즘 개선의 핵심 참조**: `ModelingEngine`의 MB-OPC 이터레이션 루프에 적응형 PID 또는 RL 기반 이동량 제어 추가 시 직접 참조
- EPE 기반 보정 피드백 루프의 수렴 판단 로직(허용 EPE 이하 달성 시 종료) 구현에 활용
- OPC 수렴 검증(convergence verification) 지표로 이터레이션별 EPE 추이 모니터링 방법 제공
- PID 계수 적응화는 다양한 레이어·패턴 유형에 대한 OPC 레시피 자동 최적화로 확장 가능

## 참고문헌
- IEEE Transactions on Semiconductor Manufacturing, 2025
- MB-OPC PID 제어 관련 선행 연구 (MEEF 기반 OPC 수렴 연구 등)

## 태그
`Verification`, `IEEE`, `MBOPC`, `PID`, `ReinforcementLearning`, `OPCConvergence`, `EPE`, `AdaptiveControl`, `FeedbackLoop`
