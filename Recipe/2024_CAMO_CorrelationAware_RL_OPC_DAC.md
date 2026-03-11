# CAMO: Correlation-Aware Mask Optimization with Modulated Reinforcement Learning

## 메타데이터
- **저자**: Xiaoxiao Liang, Haoyu Yang, Kang Liu, Bei Yu, Yuzhe Ma
- **연도**: 2024
- **게재지**: Proceedings of the 61st ACM/IEEE Design Automation Conference (DAC 2024), San Francisco, CA
- **DOI/URL**: https://doi.org/10.1145/3649329.3656254; arXiv:2404.00980
- **인용수**: ~10

## 핵심 요약
강화 학습(RL)으로 OPC 세그먼트 이동을 최적화하는 CAMO 프레임워크를 제안한다. 기존 RL 기반 OPC의 한계인 인접 세그먼트 간 공간 상관관계 무시 문제를 GNN 기반 특징 추출 + RNN 모듈로 해결하며, OPC 특화 조절(modulation)을 통한 이동 액션 선택으로 EPE를 상용 툴 대비 20% 줄이고 1.32× 속도를 달성한다.

## 주요 기여
1. 인접 세그먼트 공간 상관관계를 GNN으로 포착하는 RL 정책 구조
2. OPC 도메인 지식을 반영한 이동 액션 조절(modulation)
3. GNN 특징 추출 + RNN 순차 결정으로 복잡한 OPC 패턴 처리
4. 상용 툴 대비 EPE 20% 감소, 1.32× 가속

## Recipe/Process Flow 상세

### 기존 RL-OPC의 한계
```
엣지 기반 OPC의 세그먼트 이동 문제:
  각 세그먼트를 독립적으로 최적화
  실제: 인근 세그먼트 이동 → 상호 영향 (광학 근접 효과)
  한계: 세그먼트 간 공간 상관관계 무시 → 비최적 이동

기존 RL-OPC:
  각 세그먼트: 독립 RL 에이전트
  문제: 부분 관찰 가능성(partial observability) → 비최적 정책
  글로벌 최적화 어려움

CAMO 핵심 아이디어:
  공간 상관관계 명시적 모델링 → GNN
  순차적 의사결정 → RNN
  OPC 도메인 지식 통합 → 액션 조절
```

### CAMO 정책 구조

#### GNN 기반 공간 특징 추출
```
마스크 세그먼트 그래프:
  노드: 각 세그먼트 (위치, 현재 EPE, 이동 범위)
  엣지: 근접 세그먼트 간 연결 (광학 근접 효과 범위)

GNN 특징 추출:
  각 세그먼트: 이웃 세그먼트 정보 집계
    h_v = GNN(x_v, {x_u | u ∈ N(v)})
  메시지 패싱: 광학 근접 효과 공간 범위 반영
  출력: 공간 상관관계 포함된 세그먼트 특징

효과:
  인접 세그먼트 이동 → 자동으로 상관관계 반영
  복잡한 2D 패턴: GNN이 전체 문맥 포착
```

#### RNN 순차 결정
```
OPC 이터레이션의 순차성:
  이터레이션 t: 세그먼트 이동 → 이미지 변화
  이터레이션 t+1: 변화된 상태 기반 다음 이동 결정
  → 이전 이터레이션 이력 중요

RNN (LSTM) 통합:
  입력: 현재 GNN 특징 + 이전 이터레이션 이력
  출력: 다음 세그먼트 이동 액션
  LSTM 숨김 상태: OPC 이터레이션 이력 압축
  → 이전 이동 결과를 고려한 적응적 이동
```

#### OPC 특화 액션 조절
```
OPC 도메인 지식:
  세그먼트 이동 방향: EPE 부호에 따라 결정
  이동 크기: EPE 크기, 주변 패턴 밀도에 따라 조정
  수렴 조건: EPE 감소 추이 모니터링

조절(Modulation):
  RL 정책 출력 → OPC 도메인 조절 → 최종 액션
  예: RL 출력 × f(EPE_current, iteration_count)
  → 물리적으로 타당한 이동 범위로 제한
  → OPC 수렴 가속

액션 공간:
  이산: 이동 방향 (inward/outward) + 이동 크기 (nm 단위)
  연속: 이동 변위 δ_s ∈ [δ_min, δ_max]
```

### RL 훈련
```
환경:
  상태: 현재 마스크 M, 항공 이미지 I(M), EPE 분포
  액션: 세그먼트 이동 벡터
  보상: -ΔEPE (EPE 감소량)

훈련:
  알고리즘: PPO (Proximal Policy Optimization)
  데이터: 다양한 패턴 유형 (1D, 2D, 코너, 끝단)
  보상 조성: EPE + PV Band + 마스크 복잡도 혼합

추론:
  학습된 정책 → 새 패턴에 즉시 적용
  OPC 루프: RL 정책으로 세그먼트 이동 결정
```

### 성능 결과
```
기준: 상용 OPC 툴 (Calibre 수준)

EPE:
  CAMO: 상용 툴 대비 20% EPE 감소

속도:
  CAMO: 1.32× 가속 (상용 툴 대비)

비교:
  SOTA 학술 OPC + 상용 OPC 모두 CAMO가 우수
  특히 복잡한 2D 패턴에서 GNN 공간 상관관계 효과
```

## OPC 툴 구현 관련성
- **SKOPC RL-OPC**: `skopc/modeling/mb_opc.py`에 CAMO RL 기반 세그먼트 이동 정책 추가
- **GNN 특징 추출**: `skopc/modeling/gnn/` 기존 GNN-OPC와 통합하여 세그먼트 상관관계 포착
- **RNN 이터레이션 이력**: OPC 이터레이션 이력을 LSTM으로 압축하여 적응적 이동
- **OPC 조절**: EPE 기반 이동 크기 조절로 수렴 가속

## 참고문헌
- DAC 2024; arXiv:2404.00980
- 저자 소속: CUHK (Bei Yu 그룹) + 협력
- 관련: A2-ILT (DAC 2022)
- 관련: DiffOPC (ICCAD 2024)
- 관련: GNN-OPC (SKOPC Phase 7)

## 태그
`Recipe`, `DAC`, `OPC`, `ReinforcementLearning`, `GNN`, `RNN`, `CorrelationAware`, `SegmentMovement`, `EPE`, `CUHK`, `BeiYu`, `2024`
