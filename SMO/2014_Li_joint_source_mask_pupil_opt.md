# Joint Optimization of Source, Mask, and Pupil in Optical Lithography

## 메타데이터
- **저자**: Jia Li, Edmund Y. Lam
- **연도**: 2014
- **게재지/학회**: Proc. SPIE 9052, Optical Microlithography XXVII, 90520S (31 March 2014)
- **DOI/URL**: https://doi.org/10.1117/12.2045739
- **인용수**: 다수

## 핵심 요약
소스-마스크 최적화(SMO)를 동공 위상 조작(pupil phase manipulation)으로 확장하여 소스-마스크-동공 동시 최적화(SMPO)를 제안한다. 동공 위상 함수를 Zernike 다항식 계수로 설계하여 마스크 위상 효과를 부분적으로 보상한다. 구면 수차(spherical aberration)를 최적화에 통합하여 두꺼운 마스크 위상 효과를 보상하고 기존 SMO 대비 향상된 공정 마진을 달성한다.

## 주요 기여
- SMO를 동공 위상 최적화로 확장한 SMPO(Source-Mask-Pupil Optimization) 프레임워크 제안
- Zernike 다항식으로 동공 파면 함수 설계하여 마스크 위상 효과 보상
- 1차 및 2차 구면 수차 항을 최적화에 통합
- 기존 SMO 대비 패턴 충실도 및 공정 마진 크기 향상

## 알고리즘/수식
**SMPO 이미징 모델 (동공 포함):**
$$I(x) = \sum_k \sigma_k |h_k^{pupil}(x) * m(x)|^2$$
여기서 $h_k^{pupil}$는 동공 위상 $W(f)$가 포함된 시스템 커널:
$$H^{pupil}(f) = H(f) \cdot e^{i2\pi W(f)/\lambda}$$

**Zernike 동공 위상:**
$$W(f) = \sum_{n,m} c_{nm} Z_{nm}(f)$$
여기서 $Z_{nm}$은 Zernike 다항식, $c_{nm}$은 최적화 계수.

**구면 수차 항 (primary & secondary):**
$$W_{sph}(\rho) = c_4 Z_4(\rho) + c_{11} Z_{11}(\rho)$$
여기서 $Z_4 = \sqrt{5}(6\rho^4 - 6\rho^2 + 1)$ (primary spherical)

**SMPO 목적함수:**
$$\min_{\sigma, m, \mathbf{c}} F = \sum_j EPE_j^2(\sigma, m, \mathbf{c}) + \lambda_s R_s(\sigma) + \lambda_m R_m(m) + \lambda_c \|\mathbf{c}\|^2$$

**교번 최적화:**
1. $(\sigma, m)$ 고정 → $\mathbf{c}$ 최적화 (동공 위상)
2. $\mathbf{c}$ 고정 → $(\sigma, m)$ 최적화 (SMO)
3. 수렴까지 반복

## OPC 툴 SMO 구현 관련성
- SKOPC SMO를 동공 위상 최적화로 확장할 때 직접 참고
- `skopc/smo/pupil_optimizer.py` 구현 시 Zernike 계수 기반 동공 파면 최적화 참고
- 두꺼운 마스크 효과 보상에 동공 파면 활용 방법 제시
- 수차를 최적화 변수로 도입하는 방법 설계 참고

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Li & Lam, "Efficient SMO with augmented Lagrangian," Optics Express 2013
- Ma et al., "Gradient-based joint SPMO," JM3 2015

## 태그
`SMO`, `SPIE`, `SMPO`, `pupil-optimization`, `Zernike`, `spherical-aberration`, `wavefront`, `source-mask-pupil`, `thick-mask`, `phase-compensation`, `process-window`
