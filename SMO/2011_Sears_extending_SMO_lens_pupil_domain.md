# Extending SMO into the Lens Pupil Domain

## 메타데이터
- **저자**: Monica Kempsell Sears, Germain Fenger, Julien Mailfert, Bruce Smith
- **연도**: 2011
- **게재지/학회**: Proc. SPIE 7973, Optical Microlithography XXIV, 79731B
- **DOI/URL**: https://doi.org/10.1117/12.879058
- **인용수**: 확인 필요

## 핵심 요약
기존 SMO가 원치 않는 위상 효과를 보정하지 못하는 한계를 극복하기 위해 렌즈 퓨필 평면 최적화를 SMO에 통합한다. 렌즈 1차 구면 수차(primary spherical aberration)가 FEM(초점-노광 행렬)의 대칭에 강하게 영향을 미치며, 마스크 토포그래피가 유발하는 구면 수차를 균형 잡는 최적화된 1차 구면 수차 계수를 포함하는 퓨필 함수를 제안한다. Rochester Institute of Technology.

## 주요 기여
- SMO의 퓨필 평면 확장으로 위상 효과 보정 방법론 제시
- 렌즈 구면 수차의 FEM 대칭에 대한 영향 분석
- 마스크 토포그래피 유발 수차를 퓨필 최적화로 보정
- 소스-마스크-퓨필 공동 최적화(SMPO)를 위한 RIT 방법론

## 알고리즘/수식
**퓨필 확장 SMO (SMPO) 비용함수:**
$$F_{SMPO}(\boldsymbol{\sigma}, m, \boldsymbol{a}) = \sum_j EPE_j^2(\boldsymbol{\sigma}, m, \boldsymbol{a})$$
소스 $\boldsymbol{\sigma}$, 마스크 $m$, Zernike 퓨필 계수 $\boldsymbol{a}$ 동시 최적화.

**구면 수차 퓨필 함수:**
$$\Psi(\mathbf{f}; a_9) = a_9 Z_9(\mathbf{f}) = a_9 (6\rho^4 - 6\rho^2 + 1)$$
1차 구면 수차 Zernike 항 $Z_9$ (Fringe Zernike 표기).

**마스크 토포그래피 유발 수차 보정:**
$$a_9^{opt} = \arg\min_{a_9} \|CDEF_{sym}(\boldsymbol{\sigma}^*, m^*; a_9)\|$$
FEM 대칭 $CDEF_{sym}$ (초점 의존 CD 오차 비대칭성) 최소화.

**퓨필 최적화 그래디언트:**
$$\frac{\partial F_{SMPO}}{\partial a_9} = \sum_j 2EPE_j \cdot \frac{\partial EPE_j}{\partial a_9}$$

**이미징 모델 (퓨필 수차 포함):**
$$I(x; \boldsymbol{\sigma}, m, a_9) = \sum_k \sigma_k \left|\int M(\mathbf{f}) H_k(\mathbf{f}) e^{ia_9 Z_9(\mathbf{f})} e^{i2\pi \mathbf{f} \cdot x} d\mathbf{f}\right|^2$$

## OPC 툴 SMO 구현 관련성
- SKOPC 퓨필 포함 SMPO 구현 시 퓨필 평면 SMO 확장 방법 참고
- `skopc/smo/smpo_pupil_extension.py`에 퓨필 Zernike 계수 포함 SMPO 구현
- Fühner et al. 2012 상호 SMPO, Li & Lam 2014 SMPO와 함께 소스-마스크-퓨필 최적화 계열 참고
- 마스크 토포그래피-수차 결합 분석은 Liu et al. 2015 M3D-aware SMO와 함께 참고

## 참고문헌 (핵심)
- Fühner et al., \"Mutual SMPO source mask pupil,\" SPIE 2012
- Li & Lam, \"Joint SMO pupil,\" SPIE 2014
- Coskun et al., \"Mask topography SMO advanced nodes,\" SPIE 2011

## 태그
`SMO`, `SPIE`, `SMPO`, `lens-pupil`, `pupil-optimization`, `spherical-aberration`, `Zernike`, `mask-topography`, `FEM`, `RIT`, `phase-compensation`, `source-mask-pupil`
