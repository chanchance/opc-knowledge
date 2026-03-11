# RL-OPC: Mask Optimization With Deep Reinforcement Learning

## 메타데이터
- **저자**: Xiaoxiao Liang, Yikang Ouyang, Haoyu Yang, Bei Yu, Yuzhe Ma
- **연도**: 2024
- **게재지/학회**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD), 2024
- **DOI/URL**: https://ieeexplore.ieee.org/document/10233698/ / https://dl.acm.org/doi/abs/10.1109/TCAD.2023.3309745
- **인용수**: 50+

## 핵심 요약
RL-OPC는 깊은 강화학습(Deep RL)을 마스크 최적화에 최초로 적용한 선구적 논문으로, 미분 가능한 프록시(differentiable proxy) 없이 선호 목적 함수를 직접 최적화한다. 10개의 다양한 비아 테스트 케이스에서 EPE 위반 수를 30% 감소시키고, 통합 OPC 플로우에서 Calibre 대비 EPE를 32% 감소시킨다. CAMO(2024)의 직접적 선행 연구로, ML 기반 OPC의 RL 패러다임을 확립했다.

## 주요 기여
- **최초 RL 기반 OPC**: 마스크 최적화에 RL 모델을 최초로 도입
- **직접 목적 함수 최적화**: 미분 불가능한 목적 함수를 프록시 없이 직접 최적화
- **ILT 경쟁 성능**: RL 기반으로 수치 ILT에 경쟁력 있는 마스크 생성
- **30% EPE 감소**: 10개 비아 테스트에서 EPE 위반 30% 감소, Calibre 대비 32%

## Recipe/Process Flow 상세

### RL-OPC 마스크 최적화 파이프라인

```
초기 마스크 (설계 레이아웃)
        ↓
[RL 환경(Environment) 정의]
  상태(State) s_t:
    - 현재 마스크의 세그먼트 위치 집합
    - 각 세그먼트의 EPE 값
    - 인접 세그먼트 관계

  행동(Action) a_t:
    - 각 세그먼트에 대한 이동 결정
    - 이산 행동: 안쪽(-Δ), 유지(0), 바깥쪽(+Δ)
    - Δ: 최대 이동 거리 (설정 가능)

  보상(Reward) r_t:
    r_t = -Σ EPE_violations(M_{t+1}) + bonus_term
    - EPE 위반 총합 감소가 양의 보상
    - MRC 위반 시 음의 페널티
        ↓
[DQN/PPO 기반 정책 학습]
  신경망 정책 π_θ(a|s):
    - 입력: 현재 마스크 상태 s_t
    - 출력: 각 세그먼트 행동 확률 분포
    - 아키텍처: CNN 또는 GNN 기반

  탐험-활용 균형:
    - ε-greedy 또는 소프트맥스 정책
    - 초기: 많은 탐험 → 수렴 후: 활용 집중
        ↓
[반복 최적화 에피소드]
  각 에피소드:
    1. 초기 마스크 상태 s_0
    2. 정책 π_θ로 세그먼트 이동 선택
    3. 리소그래피 시뮬레이션으로 보상 계산
    4. 경험 메모리에 (s, a, r, s') 저장
    5. 배치 샘플로 정책 업데이트
  수렴까지 반복
        ↓
최적화된 마스크 출력
```

### RL 정식화 상세

**MDP (마르코프 결정 과정)**:
- 상태 공간: 모든 가능한 마스크 세그먼트 위치 집합
- 행동 공간: 각 세그먼트에 대한 이산 이동 결정
- 전이 모델: 세그먼트 이동 → 새 마스크 → 리소그래피 시뮬레이션
- 보상 모델: EPE 감소량 + 제약 위반 패널티

**DQN 변형 적용**:
- 경험 재생(Experience Replay) 버퍼
- 타겟 네트워크(Target Network)로 학습 안정화
- 이중 DQN(Double DQN)으로 Q값 과대 추정 방지

### 통합 OPC 플로우
RL-OPC + 추가 정제 단계의 통합 플로우:
```
레이아웃 → RL-OPC (초기 마스크) → 소수 수치 OPC 반복 → 최종 마스크
```
- RL-OPC가 좋은 초기 마스크 제공
- 소수 추가 OPC 반복으로 세밀한 보정
- 통합 플로우에서 Calibre 대비 EPE 32% 감소

### 성능 결과 (10개 비아 테스트 케이스)
| 방법 | EPE 위반 수 | 대비 |
|------|-----------|------|
| Calibre (기준) | 기준 | - |
| GAN-OPC | 높음 | - |
| RL-OPC | -30% | Calibre 대비 |
| RL-OPC + 정제 | **-32%** | Calibre 대비 |

### RL vs 기존 ML OPC 비교
| 방법 | 탐색 능력 | 미분 불가 목적함수 | 새 패턴 적응 |
|------|---------|-----------------|-----------|
| GAN-OPC | 없음 | 불가 | 재학습 필요 |
| DAMO | 없음 | 불가 | 재학습 필요 |
| RL-OPC | 있음 | 가능 | 재학습 최소 |

## OPC 툴 구현 관련성
RL-OPC는 SKOPC의 모델 OPC 및 레시피 탐색에 활용 가능:
- **레시피 파라미터 RL 탐색**: OPC 레시피의 파라미터 공간을 RL로 탐색하여 자동 최적화
- **비미분 목적함수 최적화**: DRC 위반 수 등 미분 불가 지표를 직접 최적화
- **세그먼트 이동 정책**: GNN-OPC의 세그먼트 이동 결정에 RL 정책 통합
- **CAMO 전 단계**: CAMO(2024)의 공간 상관관계 개선 전, RL-OPC를 기본 구현으로 참조

## 참고문헌 (핵심)
- Mnih et al., "Human-level control through deep reinforcement learning" (Nature 2015)
- Schulman et al., "Proximal Policy Optimization" (2017)
- Yang et al., "GAN-OPC" (IEEE TCAD 2020)
- Liang et al., "CAMO" (DAC 2024) - 후속 연구

## 태그
`RL-OPC`, `Reinforcement Learning`, `DQN`, `Mask Optimization`, `OPC`, `EPE`, `Segment Movement`, `IEEE TCAD`, `2024`, `Direct Optimization`, `No Differentiable Proxy`
