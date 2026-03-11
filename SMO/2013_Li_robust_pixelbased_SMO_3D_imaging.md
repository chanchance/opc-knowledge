# Robust Pixel-Based Source and Mask Optimization for Inverse Lithography

## 메타데이터
- **저자**: Sikun Li, Xiangzhao Wang, Yan Bu
- **연도**: 2013
- **게재지/학회**: Optics & Laser Technology, Vol. 45, pp. 285–293
- **DOI/URL**: https://doi.org/10.1016/j.optlastec.2012.07.001
- **인용수**: 다수

## 핵심 요약
3D 부분 결맞음 이미징 모델을 사용하여 공정 변동(디포커스, 도즈, 수차, 방사 보정, 아포다이제이션)을 통합한 강인한 픽셀 기반 SMO 방법을 제안한다. 패턴 오차 기대값(expectation of pattern error)을 비용함수로 사용하여 공칭 조건이 아닌 실제 제조 환경에서의 강인성을 향상시킨다. 기존 픽셀 기반 SMO의 명목 조건 최적화 한계를 극복한다.

## 주요 기여
- 3D 부분 결맞음 이미징 모델로 현실적 공정 조건 반영
- 패턴 오차 기대값을 비용함수로 사용하는 강인 SMO 정식화
- 디포커스, 도즈, 수차, 방사 보정, 아포다이제이션 통합
- 공칭 조건 최적화 대비 실제 제조 환경에서 우수한 강인성 실증

## 알고리즘/수식
**강인 SMO 비용함수 (패턴 오차 기대값):**
$$F_{robust} = \mathbb{E}_{(\delta f, \delta d, \delta a)}\left[\sum_j EPE_j^2(\boldsymbol{\sigma}, m; \delta f, \delta d, \delta a)\right]$$
디포커스 $\delta f$, 도즈 $\delta d$, 수차 $\delta a$의 확률 분포에 대한 기대값.

**3D 부분 결맞음 이미징 모델:**
$$I(x; \delta f, \delta a) = \sum_k \sigma_k |h_k(\cdot; \delta f, \delta a) * m|^2(x)$$
디포커스와 수차를 포함한 3D 커널 $h_k$로 에어리얼 이미지 계산.

**기대값 근사 (이산 샘플링):**
$$F_{robust} \approx \frac{1}{N_{cond}} \sum_{i=1}^{N_{cond}} \sum_j EPE_j^2(\boldsymbol{\sigma}, m; \delta f_i, \delta d_i)$$
대표 공정 조건 $N_{cond}$개 샘플로 기대값 근사.

**그래디언트 (강인 비용함수):**
$$\frac{\partial F_{robust}}{\partial \sigma_k} = \frac{1}{N_{cond}} \sum_i \sum_j \frac{\partial EPE_j^2}{\partial \sigma_k}\bigg|_{cond_i}$$

**방사 보정 및 아포다이제이션 포함 TCC:**
$$TCC(f_1, f_2) = \int\int J(f) \cdot A(f+f_1) \cdot A^*(f+f_2) \cdot P(f+f_1) \cdot P^*(f+f_2) df$$
방사 함수 $A$와 동공 함수 $P$ 포함.

## OPC 툴 SMO 구현 관련성
- SKOPC 강인 SMO에서 3D 이미징 모델 기반 공정 변동 통합 방법 참고
- `skopc/smo/robust_smo_3d.py`에 디포커스/도즈/수차 포함 강인 비용함수 구현
- 공정 변동 샘플링 기반 기대값 근사는 실제 HVM 환경 SMO에 필수
- Hashimoto et al. 2013 RSMO와 함께 강인 SMO 방법론 비교 참고

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Jia & Lam, "Pixelated SMO process robustness," Optics Express 2011
- Hashimoto et al., "Robust SMO HVM," SPIE 2013

## 태그
`SMO`, `Optics-Laser-Technology`, `robust-SMO`, `pixel-based`, `3D-imaging`, `process-variation`, `defocus`, `dose`, `aberration`, `expectation-cost`, `partial-coherence`
