# CAMO: Correlation-Aware Mask Optimization with Modulated Reinforcement Learning

## 메타데이터
- **저자**: Xiaoxiao Liang, Haoyu Yang, Kang Liu, Bei Yu, Yuzhe Ma
- **연도**: 2024
- **게재지/학회**: Design Automation Conference (DAC 2024), arXiv:2404.00980
- **DOI/URL**: https://arxiv.org/abs/2404.00980
- **인용수**: N/A (2024 신규)

## 핵심 요약
CAMO는 OPC 문제의 도메인 고유 특성을 강화학습(RL)에 명시적으로 통합한 마스크 최적화 시스템이다. 기존 RL-OPC가 순수 데이터 기반으로 OPC 문제의 특수성을 무시한 반면, CAMO는 인접 세그먼트 이동의 공간적 상관관계와 OPC 영감 행동 조절(modulation)을 통합하여 학술 및 산업 최고 수준 OPC 엔진 대비 우수한 성능을 달성한다.

## 주요 기여
- **공간 상관관계 통합**: 인접 마스크 세그먼트 이동 간의 공간적 의존성을 RL 프레임워크에 명시적 통합
- **OPC 영감 행동 조절**: 제조 도메인 지식을 RL 행동 선택에 내재화
- **도메인 인식 RL**: 순수 데이터 기반 ML의 한계를 극복하는 OPC 특화 RL 설계
- **SOTA 초과 성능**: 비아 및 금속 레이어 모두에서 학술/산업 OPC 엔진 능가

## Recipe/Process Flow 상세

### CAMO RL 기반 OPC 최적화 파이프라인

```
초기 마스크 (설계 레이아웃)
        ↓
[환경 모델링]
  상태(State): 현재 마스크 세그먼트 위치 집합
  {s_i = (x_i, y_i) | i = 1..N 세그먼트}

[CAMO 에이전트]
  ┌─────────────────────────────┐
  │  공간 상관관계 모듈           │
  │  - 인접 세그먼트 그래프 구성  │
  │  - GNN/Attention으로 상관관계 │
  │    인코딩                   │
  │                             │
  │  OPC 행동 조절 모듈          │
  │  - 리소그래피 기반 이동 방향  │
  │    바이어스                  │
  │  - 제조 규칙 기반 행동 마스킹 │
  └─────────────────────────────┘
        ↓
행동(Action): 각 세그먼트의 이동량 δ_i ∈ {-Δ, 0, +Δ}

보상(Reward):
  r = -EPE_total + λ·ΔPVB - γ·MRC_violations

[환경 전이]
  마스크 업데이트 → 리소그래피 시뮬레이션 → 다음 상태

[반복 최적화]
  에이전트가 최대 보상 정책 학습
        ↓
최적화된 마스크
```

### RL 정식화 상세

**상태 공간 (State Space)**:
- 각 마스크 세그먼트의 현재 x, y 좌표
- 리소그래피 시뮬레이션 결과 (EPE, 공중 이미지 특성)
- 인접 세그먼트와의 상대적 위치

**행동 공간 (Action Space)**:
- 각 세그먼트에 대해 이산적 이동: 안쪽(-Δ), 유지(0), 바깥쪽(+Δ)
- OPC 영감 조절로 비효율적 행동 사전 제거

**보상 함수 (Reward Function)**:
$$r_t = -\text{EPE}_{total} + \lambda_1 \cdot \Delta\text{PVB} - \lambda_2 \cdot \text{MRC\_violations} - \lambda_3 \cdot \text{ShotCount}$$

**공간 상관관계 모델링**:
인접 세그먼트 간의 이동이 서로 영향을 미치는 현상을 포착:
- 한 세그먼트 이동 시 인접 세그먼트의 최적 이동 방향이 변화
- GNN 또는 어텐션 메커니즘으로 이 상관관계를 에이전트에게 인식

### OPC 영감 행동 조절
모델 기반 OPC의 도메인 지식을 RL에 통합:
1. 리소그래피 시뮬레이션에서 EPE 방향 추출
2. EPE 감소 방향으로 이동 확률 증폭
3. MRC 위반 가능성이 있는 이동 억제
4. 수렴 가속 및 샘플 효율 향상

### 비교 성능 (비아/금속 레이어)
- RL-OPC 대비: 수렴 속도 향상, EPE 감소
- GAN-OPC/DAMO 대비: 새 디자인 탐색 능력 보유
- 상용 OPC 툴 대비: 유사 또는 우수한 품질

## OPC 툴 구현 관련성
CAMO의 RL 접근법은 SKOPC PWO 및 Recipe Runner에 응용 가능:
- **레시피 파라미터 탐색**: RL 에이전트로 최적 OPC 레시피 파라미터 자동 탐색
- **공정 윈도우 최적화**: SKOPC PWO 모듈에 RL 기반 최적화 전략 통합
- **세그먼트 이동 정책**: GNN-OPC의 세그먼트 이동 결정에 RL 정책 적용
- **도메인 지식 통합**: SKOPC의 rule_opc.py 지식을 RL 보상 함수에 인코딩

## 참고문헌 (핵심)
- Ma et al., "RL-OPC: Mask Optimization with Deep Reinforcement Learning" (IEEE TCAD 2023)
- Chen et al., "DAMO: Deep Agile Mask Optimization" (ICCAD 2020)
- Yang et al., "GAN-OPC" (IEEE TCAD 2020)
- Sutton & Barto, "Reinforcement Learning: An Introduction" (MIT Press, 2018)
- Mnih et al., "Human-level control through deep reinforcement learning" (Nature, 2015)

## 태그
`CAMO`, `Reinforcement Learning`, `Mask Optimization`, `OPC`, `Spatial Correlation`, `DAC 2024`, `2024`, `Domain-aware RL`, `Segment Movement`, `EPE`, `MRC`
