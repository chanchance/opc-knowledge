# Source Mask Optimization Using Real-Coded Genetic Algorithms

## 메타데이터
- **저자**: Fan Yang, Jun Wang, Jia Li, Andreas Erdmann
- **연도**: 2013
- **게재지/학회**: Proc. SPIE 8683, Optical Microlithography XXVI, 86831T (12 April 2013)
- **DOI/URL**: https://doi.org/10.1117/12.2010137
- **인용수**: 다수

## 핵심 요약
소스-마스크 동시 최적화에 실수 코딩 유전 알고리즘(Real-Coded Genetic Algorithm, RCGA)을 적용하는 방법을 제안한다. 그래디언트 계산 없이 픽셀화 소스와 마스크를 동시 최적화하며, 패턴 오차를 40~70% 감소시키는 결과를 실증한다. 유전 알고리즘 특성상 지역 최솟값 함정을 회피하는 전역 탐색 능력을 제공하며, 기존 그래디언트 기반 SMO의 보완적 대안으로 활용 가능하다.

## 주요 기여
- 그래디언트 불필요한 RCGA 기반 SMO 구현으로 전역 최적화 가능
- 픽셀화 소스와 이진 마스크 동시 최적화
- 패턴 오차 40~70% 감소 실증
- 지역 최솟값 문제를 회피하는 메타휴리스틱 SMO 접근 제시

## 알고리즘/수식
**실수 코딩 유전 알고리즘 SMO:**
$$\min_{\boldsymbol{\sigma}, m} F(\boldsymbol{\sigma}, m) = \sum_j EPE_j^2(\boldsymbol{\sigma}, m)$$
그래디언트 없이 진화 연산자(선택, 교차, 변이)로 최적화.

**RCGA 염색체 인코딩:**
$$\text{chromosome} = [\sigma_1, \sigma_2, \ldots, \sigma_{N_{src}}, m_1, m_2, \ldots, m_{N_{mask}}]$$
소스 픽셀 강도 $\sigma_k \in [0,1]$와 마스크 픽셀 $m_j \in \{0,1\}$을 연결.

**적합도 함수 (Fitness Function):**
$$\text{fitness} = \frac{1}{F(\boldsymbol{\sigma}, m)} = \frac{1}{\sum_j EPE_j^2}$$
낮은 패턴 오차 = 높은 적합도.

**선택 (Selection):**
토너먼트 선택 또는 룰렛 휠 선택으로 우수 개체 선발.

**교차 (Crossover):**
$$\sigma_k^{child} = \alpha \sigma_k^{parent_1} + (1-\alpha) \sigma_k^{parent_2}, \quad \alpha \in [0,1]$$
실수 블렌딩 교차(BLX-α)로 소스 값 유전.

**변이 (Mutation):**
$$\sigma_k \leftarrow \sigma_k + \mathcal{N}(0, \sigma_{mut}^2)$$
가우시안 변이로 다양성 유지.

**수렴 기준:**
패턴 오차 감소율: 40~70% (그래디언트 기반 대비 경쟁적 결과).

## OPC 툴 SMO 구현 관련성
- SKOPC SMO 모듈에 그래디언트 없는 대안 최적화 방법 추가 시 참고
- `skopc/smo/ga_smo.py` 구현으로 지역 최솟값 회피 능력 확보 가능
- 그래디언트 기반 SMO와 하이브리드 조합(전역 RCGA → 로컬 그래디언트 정밀화) 설계 참고
- 이진 마스크 변수와 연속 소스 변수의 혼합 최적화 전략 참고

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Hsu et al., "An innovative SMO method," Proc. SPIE 7140, 2008
- Shi et al., "PSO-GA hybrid source optimization," IEEE Photonics J. 2023

## 태그
`SMO`, `SPIE`, `genetic-algorithm`, `RCGA`, `real-coded-GA`, `metaheuristic`, `gradient-free`, `global-optimization`, `pixelated-source`, `binary-mask`, `EPE`, `evolutionary-computation`
