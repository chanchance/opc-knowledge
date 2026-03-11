# Robust Source and Mask Optimization Compensating for Mask Topography Effects in Computational Lithography

## 메타데이터
- **저자**: Jia Li, Edmund Y. Lam
- **연도**: 2014
- **게재지/학회**: Optics Express, Vol. 22, No. 8, pp. 9471–9485
- **DOI/URL**: https://doi.org/10.1364/OE.22.009471
- **인용수**: 다수

## 핵심 요약
마스크 토포그래피(3D 마스크) 효과를 보상하는 강인한 SMO 방법을 제안한다. 동공 파면 수차를 SMO 프로시저에 통합하여 사용 가능한 DOF(uDOF)를 최대화하는 대안적 접근을 사용한다. Zernike 다항식 계수를 통해 1차 및 2차 구면 수차를 동공 파면 함수에 추가하고, 켤레 그래디언트로 수차 동공 조건에서 최적 소스-마스크 쌍을 달성한다.

## 주요 기여
- 마스크 토포그래피 효과를 동공 수차로 모델링하여 SMO에 통합
- Zernike 구면 수차 계수를 SMO 강인성 파라미터로 활용
- 켤레 그래디언트 기반 수차 동공 조건 최적 소스-마스크 달성
- 마스크 토포그래피 및 유사 이미징 효과에 대한 강인성 동시 달성

## 알고리즘/수식
**수차 포함 이미징 모델:**
$$I(x; W) = \sum_k \sigma_k |h_k(\cdot; W) * m|^2(x)$$
동공 파면 수차 $W(f,g)$를 포함한 커널 $h_k$.

**Zernike 파면 수차:**
$$W(f,g) = \sum_{n,m} c_{nm} Z_{nm}(f,g)$$
구면 수차 Zernike 항:
- 1차 구면 수차: $Z_{11} = \sqrt{5}(6\rho^4 - 6\rho^2 + 1)$
- 2차 구면 수차: $Z_{22}$ (고차 항)

**강인 SMO 비용함수 (uDOF 최대화):**
$$\min_{\boldsymbol{\sigma}, m} F_{robust} = F_{nominal}(\boldsymbol{\sigma}, m) + \lambda_W \sum_{nm} c_{nm}^2 F_{aberr}(\boldsymbol{\sigma}, m; c_{nm})$$

**수차 민감도 통합:**
$$F_{aberr} = \sum_j \left(\frac{\partial I(x_j; W)}{\partial c_{nm}} \cdot \Delta c_{nm}\right)^2$$
각 Zernike 계수 변동 $\Delta c_{nm}$에 대한 이미지 민감도.

**켤레 그래디언트 업데이트:**
$$d_\sigma^{(t)} = -\nabla_\sigma F_{robust}^{(t)} + \beta^{(t)} d_\sigma^{(t-1)}$$
$$d_m^{(t)} = -\nabla_m F_{robust}^{(t)} + \beta^{(t)} d_m^{(t-1)}$$

**마스크 토포그래피 ↔ 동공 수차 등가성:**
두꺼운 마스크의 3D 효과를 등가 동공 수차로 근사:
$$W_{M3D}(f,g) \approx \sum_{nm} c_{nm}^{M3D} Z_{nm}(f,g)$$

## OPC 툴 SMO 구현 관련성
- SKOPC EUV/DUV SMO에서 마스크 3D 효과를 동공 수차로 근사 처리 시 참고
- `skopc/smo/aberration_robust_smo.py`에 Zernike 수차 포함 강인 SMO 구현
- 마스크 토포그래피 보상은 `skopc/litho/m3d_aberration.py`로 모듈화 가능
- Li & Lam 2013 증강 라그랑지안 SMO와 함께 동일 그룹의 발전된 연구로 참고

## 참고문헌 (핵심)
- Li & Lam, "Efficient SMO augmented Lagrangian," Optics Express 2013
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Ma et al., "EUV SMO M3D," IEEE TCI 2019

## 태그
`SMO`, `Optics-Express`, `robust-SMO`, `mask-topography`, `M3D`, `Zernike`, `pupil-aberration`, `spherical-aberration`, `conjugate-gradient`, `uDOF`, `computational-lithography`
