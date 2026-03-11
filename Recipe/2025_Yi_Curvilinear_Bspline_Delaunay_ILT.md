# Curvilinear Mask Optimization for Inverse Lithography Based on B-splines and Delaunay Triangulation

## 메타데이터
- **저자**: Xiaoru Yi, Junqing Chen
- **연도**: 2025
- **게재지/학회**: arXiv preprint, arXiv:2504.11962
- **DOI/URL**: https://arxiv.org/html/2504.11962
- **기관**: Department of Mathematical Sciences, Tsinghua University

## 핵심 요약
본 논문은 주기적 B-스플라인 곡선으로 포토마스크 경계를 표현하고 Delaunay 삼각분할을 통해 수치 적분 노드와 제어점 간의 명시적 그래디언트 공식을 유도하는 역리소그래피 마스크 최적화 기법을 제시한다. 픽셀 기반 ILT 대비 최적화 변수 수를 대폭 감소시키며, 현대 마스크 라이터로 제조 가능한 매끄러운 커빌리니어 마스크를 생성한다. O(h²) 수렴률의 엄밀한 오차 경계를 수학적으로 증명하며, 5개 수치 예제로 실현 가능성을 검증한다.

## 주요 기여
- **B-스플라인 마스크 표현**: 주기적 B-스플라인으로 마스크 경계 표현, 픽셀 기반 대비 변수 수 대폭 감소
- **Delaunay 삼각분할 연계**: 스플라인 경계 내부를 삼각 메시로 이산화하여 효율적 수치 적분 구현
- **명시적 그래디언트 공식**: 목적 함수 그래디언트와 제어점 이동의 수학적 명시적 관계 유도
- **엄밀한 오차 경계**: 다각형 근사의 O(h²) 수렴률 수학적 증명

## Recipe/Process Flow 상세

### B-스플라인 기반 ILT 최적화 플로우

```
초기 마스크 경계 설정
  - 설계 레이아웃에서 초기 경계 제어점 샘플링
  - 주기적 B-스플라인으로 곡선 매개변수화
  - 제어점: P = {P₀, P₁, ..., P_{n-1}} (주기적)
        ↓
[Delaunay 삼각분할]
  - B-스플라인 경계로 둘러싸인 영역을 삼각형 메시로 분할
  - Gaussian 적분 포인트와 제어점 간 매핑 구성
  - 삼각분할 갱신: 제어점 이동 시 메시 재생성
        ↓
[순방향 리소그래피 시뮬레이션]
  - B-스플라인 마스크 M_spline에서 이진 마스크 근사
  - 컨볼루션 기반 리소그래피 이미징:
    I(x,y) = |∫∫ h(x-x', y-y') · M(x',y') dx'dy'|²
  - Gaussian 적분으로 수치 계산
        ↓
[명시적 그래디언트 계산]
  목적 함수: L = ||I_wafer - T||²
  제어점 그래디언트: ∂L/∂P_i = Σ_j (∂L/∂I_j)(∂I_j/∂P_i)
  Delaunay 삼각분할을 통한 연쇄 법칙 적용
        ↓
[그래디언트 기반 제어점 업데이트]
  P_{t+1} = P_t - α · ∂L/∂P_t
  (Adam 또는 L-BFGS 최적화)
        ↓
[수렴 판단]
  ||∂L/∂P|| < ε 또는 최대 반복 횟수
        ↓
최적화된 커빌리니어 마스크 (B-스플라인 표현)
```

### B-스플라인 마스크 표현 수학적 정의

주기적 B-스플라인 곡선:
$$\mathbf{C}(t) = \sum_{i=0}^{n-1} N_{i,k}(t) \cdot \mathbf{P}_i, \quad t \in [0,1]$$

- $N_{i,k}$: k차 B-스플라인 기저 함수
- $\mathbf{P}_i$: 제어점 (최적화 변수)
- 주기성: $\mathbf{P}_n = \mathbf{P}_0$ (폐곡선)

### 오차 경계
다각형 근사의 O(h²) 수렴:
$$|\text{Area}(M_{spline}) - \text{Area}(M_{polygon})| = O(h^2)$$
여기서 h는 삼각분할 메시 크기

### 픽셀 기반 ILT vs B-스플라인 비교
| 특성 | 픽셀 기반 ILT | B-스플라인 기반 |
|------|--------------|----------------|
| 최적화 변수 수 | N²(픽셀 수) | ~수백(제어점 수) |
| 마스크 매끄러움 | 계단형(Manhattan) | 연속 곡선 |
| 제조 가능성 | 후처리 필요 | 직접 사용 가능 |
| 수렴 속도 | 느림(고차원) | 빠름(저차원) |
| 수학적 보장 | 없음 | O(h²) 오차 경계 |

## OPC 툴 구현 관련성
B-스플라인 커빌리니어 마스크는 SKOPC 고급 기능에 활용 가능:
- **커빌리니어 마스크 지원**: SKOPC 레이아웃 에디터에 B-스플라인 마스크 표현 추가
- **EUV OPC**: EUV 고 NA에서 커빌리니어 마스크의 우수한 공정 윈도우 활용
- **ILT 가속**: 픽셀 기반 대비 적은 변수로 SKOPC ILT 최적화 가속
- **수학적 엄밀성**: O(h²) 수렴 보장으로 SKOPC 검증 방법론 강화

## 참고문헌 (핵심)
- de Boor, "A Practical Guide to Splines" (Springer, 2001)
- Delaunay, "Sur la sphère vide" (1934)
- Yang et al., "GPU-Accelerated Inverse Lithography" (ISPD 2025)
- Chen et al., "DiffOPC" (ICCAD 2024)
- Granik, "Fast Pixel-Based Mask Optimization for Inverse Lithography" (JM3 2006)

## 태그
`Curvilinear Mask`, `B-spline`, `Delaunay Triangulation`, `ILT`, `Inverse Lithography`, `Gradient Optimization`, `Mask Optimization`, `OPC`, `arXiv 2025`, `Tsinghua`, `Mathematical Rigor`
