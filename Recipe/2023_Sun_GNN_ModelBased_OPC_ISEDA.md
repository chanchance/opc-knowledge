# Efficient Model-Based OPC via Graph Neural Network

## 메타데이터
- **저자**: Shuyuan Sun, Xuelian Chen, Fan Yang, Xuan Zeng (+ Bei Yu 그룹, CUHK)
- **연도**: 2023
- **게재지**: IEEE/ACM International Symposium of EDA (ISEDA 2023)
- **DOI/URL**: https://ieeexplore.ieee.org/document/10218720/
- **인용수**: ~20

## 핵심 요약
그래프 신경망(GNN)을 활용하여 모델 기반 OPC의 초기 마스크 보정 예측을 가속화하는 연구. 칩 레이아웃을 그래프로 표현(세그먼트=노드, 회절 효과=에지)하고, GNN이 각 세그먼트의 임베딩을 학습하여 최적 이동량(shift value)을 예측함으로써 MB-OPC의 이터레이션 수를 크게 줄인다. SKOPC의 `skopc/modeling/gnn/`과 직접적으로 연관되는 방법론이다.

## 주요 기여
1. 칩 레이아웃의 그래프 모델 설계 (세그먼트-노드, 회절-에지)
2. GNN 기반 세그먼트 임베딩 학습 및 이동량 예측
3. GNN 예측으로 초기 보정값 설정 → OPC 이터레이션 수 감소
4. 전체 칩 규모 마스크에서 더 적은 이터레이션으로 수렴 달성

## Recipe/Process Flow 상세

### 레이아웃의 그래프 표현
```
노드(Node) = 레이아웃 에지 세그먼트
- 노드 피처: 세그먼트 위치, 길이, CD, 로컬 밀도 정보

에지(Edge) = 세그먼트 간 회절 효과
- 에지 가중치: 두 세그먼트 사이의 광학적 상호작용 강도
- 연결 기준: 근방 세그먼트 (특정 반경 이내)

그래프 G = (V, E)
V = {segment_1, ..., segment_N}
E = {(i,j) | dist(i,j) < r_cutoff}
```

### GNN 기반 OPC 예측
```
GNN 포워드 패스:
1. 노드 임베딩 초기화: h_i^(0) = f_init(node_features_i)

2. 메시지 패싱 (L 레이어):
   m_i^(l) = AGG({h_j^(l-1) · w_ij | j ∈ N(i)})
   h_i^(l) = UPDATE(h_i^(l-1), m_i^(l))

   여기서 w_ij = 에지 가중치 (회절 효과)

3. 이동량 예측:
   shift_i = f_pred(h_i^(L))

4. 예측된 shift_i를 초기 OPC 보정값으로 사용
```

### GNN 가속 MB-OPC 흐름
```
기존 MB-OPC:
  초기 마스크 → 이터레이션 1 → ... → 이터레이션 N (수렴)

GNN 가속 MB-OPC:
  초기 마스크 + GNN 예측 → 개선된 초기 마스크
                           → 이터레이션 1 → ... → 이터레이션 N' (수렴)
                           (N' < N)
```

### 성능 이점
```
이터레이션 수: N → N' (N' < N, 수렴 가속)
EPE 품질: 동등 또는 향상
런타임: 이터레이션 감소로 전체 런타임 단축
확장성: 전체 칩 규모 마스크에 적용 가능
```

### 훈련 세부 사항
- 훈련 데이터: 기존 MB-OPC 솔루션 (레이아웃 → 최적 shift 쌍)
- 손실 함수: MSE(예측 shift, 최적 shift)
- 일반화: 다양한 레이어/패턴 유형에 전이 학습 가능

## OPC 툴 구현 관련성
- **SKOPC GNN-OPC 직접 연관**: `skopc/modeling/gnn/` ResGNN과 동일한 개념 — 세그먼트 변위 예측
- **그래프 구성**: 레이아웃을 세그먼트 그래프로 변환하는 전처리 파이프라인 참조
- **초기 보정 가속**: SKOPC OPC 이터레이션 루프의 초기값 설정에 GNN 예측 활용 가능
- **CUHK Bei Yu 그룹**: OpenILT, CTM-SRAF, MB-OPC Extension과 동일 그룹의 일관된 연구

## 참고문헌
- IEEE ISEDA 2023, Document 10218720
- PDF: http://www.cse.cuhk.edu.hk/~byu/papers/C160-ISEDA2023-OPC.pdf
- 관련: Model-based OPC Extension in OpenILT (IEEE ISEDA 2024)
- 관련: GNN-OPC (skopc/modeling/gnn/)

## 태그
`Recipe`, `IEEE`, `GNN`, `ModelBasedOPC`, `GraphNeuralNetwork`, `IterationReduction`, `SegmentPrediction`, `Bei-Yu`, `CUHK`, `2023`
