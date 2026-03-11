# Fast Curvilinear Optical Proximity Correction Adopting Quasi-Uniform B-Spline Curves

## 메타데이터
- **저자**: He Yang et al.
- **연도**: 2024
- **게재지**: Proc. SPIE 13423, Optical Microlithography XXXVII (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3052XXX

## 핵심 요약
준균일 B-스플라인(quasi-uniform B-spline) 곡선을 채택한 빠른 곡선형 OPC 방법을 제안한다. 기존 맨해튼 OPC 대비 곡선형 패턴을 효율적으로 표현하고, 제어점 수를 최소화하면서 정밀한 엣지 기술(edge description)을 달성하여 OPC 런타임과 데이터 볼륨을 최적화한다.

## 주요 기여
1. **준균일 B-스플라인 표현**: OPC 엣지를 준균일 B-스플라인으로 기술하여 제어점 최소화
2. **빠른 곡선형 OPC**: B-스플라인 기반 OPC로 런타임 단축
3. **데이터 볼륨 최적화**: 맨해튼 대비 효율적인 곡선형 데이터 표현
4. **정확도-속도 트레이드오프**: 제어점 수와 OPC 정밀도 간 최적 균형

## 알고리즘/수식
### 준균일 B-스플라인 OPC 표현
```
B-스플라인 곡선:
  C(t) = Σ_{i=0}^{n} N_{i,k}(t) · P_i

여기서:
  P_i: 제어점 (OPC 최적화 변수)
  N_{i,k}(t): B-스플라인 기저 함수 (차수 k)
  t: 파라미터 (0 ≤ t ≤ 1)

준균일 노트 벡터:
  T = [0,...,0, t_1, t_2, ..., t_{n-k}, 1,...,1]
  → 균일 분포 + 양 끝 클램프

OPC 최적화:
  min_{P_i} Σ_j ||CD_sim(P_i) - CD_target||²
  subject to: MRC (제어점 간 최소 간격 ≥ MRC_min)
```

### 데이터 볼륨 비교
```
맨해튼 OPC: N_vertex 개 꼭짓점 (직각 구석마다 1개)
B-스플라인 OPC: N_ctrl 개 제어점 (N_ctrl << N_vertex)

데이터 감소율 = N_ctrl / N_vertex
목표: EUV 곡선형 마스크 데이터 볼륨 최소화
```

## OPC 툴 SMO 구현 관련성
- 곡선형 OPC 표현 방법: SKOPC에서 B-스플라인 기반 마스크 표현 채택 가능
- 제어점 기반 최적화: 맨해튼 → 곡선형 OPC 전환 시 핵심 알고리즘
- 빠른 런타임: 준균일 B-스플라인으로 전체 칩 곡선형 OPC 가능성
- EUV 테이프아웃 데이터 볼륨 관리 방향

## 태그
`OPC`, `curvilinear`, `B_spline`, `quasi_uniform`, `EUV`, `data_volume`, `runtime`, `mask_representation`, `SPIE`
