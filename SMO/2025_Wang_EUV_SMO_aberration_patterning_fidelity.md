# Patterning Fidelity Enhancement and Aberration Mitigation in EUV Lithography Through Source–Mask Optimization

## 메타데이터
- **저자**: Q. Wang, Q. Wu, Y. Li, X. Liu, Y. Li
- **연도**: 2025
- **게재지/학회**: Micromachines (MDPI), Vol. 16, No. 10, 1166
- **DOI/URL**: https://doi.org/10.3390/mi16101166
- **인용수**: 확인 필요

## 핵심 요약
켤레 기울기(conjugate gradient) 방법으로 마스크 패턴과 소스 형상을 반복 최적화하는 SMO 프레임워크를 사용하여 EUV 리소그래피에서 패턴 전사 정확도를 향상시키고 수차를 동시에 경감한다. 40nm 최소 피치(2nm 노드 BEOL 대표) 패턴에서 CD 균일성 변동 4.02% 감소, 노광 위도(EL) 1.48% 향상, MEF 5.45% 감소를 달성한다.

## 주요 기여
- SMO 기반 EUV 패턴 전사 정확도 향상 및 수차 경감 통합 프레임워크
- 켤레 기울기 알고리즘으로 소스-마스크 반복 최적화
- CD 균일성 4.02% 개선, EL 1.48% 향상, MEF 5.45% 감소
- 2nm 노드 BEOL 40nm 피치 패턴 검증

## 알고리즘/수식
**EUV SMO 비용함수 (수차 포함):**
$$F(\boldsymbol{\sigma}, m) = \sum_j \left(I_j(\boldsymbol{\sigma}, m) - I_{target,j}\right)^2 + \lambda_{aber} \sum_n S_n^2(\boldsymbol{\sigma}, m)$$
EPE 충실도 항 + 수차 민감도 페널티 $S_n^2$ 포함.

**수차 민감도 지표:**
$$S_n = \frac{\partial CD}{\partial a_n}\bigg|_{a_n=0}$$
Zernike 수차 계수 $a_n$에 대한 CD 민감도.

**켤레 기울기 최적화:**
$$\boldsymbol{\sigma}^{(t+1)} = \boldsymbol{\sigma}^{(t)} + \alpha_t^s d_t^s, \quad m^{(t+1)} = m^{(t)} + \alpha_t^m d_t^m$$
켤레 기울기 방향 $d_t$으로 업데이트.

**EUV 이미징 모델 (수차 Zernike 포함):**
$$I(x; \boldsymbol{\sigma}, m, \boldsymbol{a}) = \sum_k \sigma_k \left|\int M(\mathbf{f}) H_k(\mathbf{f}) e^{i\Psi(\mathbf{f};\boldsymbol{a})} e^{i2\pi \mathbf{f} \cdot x} d\mathbf{f}\right|^2$$
$$\Psi(\mathbf{f};\boldsymbol{a}) = \sum_n a_n Z_n(\mathbf{f})$$

**성능 지표:**
- CD 균일성 변동 감소: 4.02%
- 노광 위도(EL) 향상: 1.48%
- 마스크 오차 인자(MEF) 감소: 5.45%

## OPC 툴 SMO 구현 관련성
- SKOPC EUV SMO에서 수차 경감 + 패턴 충실도 향상 통합 프레임워크 참고
- `skopc/smo/euv_aberration_smo.py`에 수차 민감도 페널티 포함 EUV SMO 구현
- 켤레 기울기 최적화는 `skopc/smo/conjugate_gradient_smo.py`에 구현
- Li et al. 2017 LASSMO, Ma et al. 2019 EUV gradient SMO와 함께 수차 강인 EUV SMO 계열 참고

## 참고문헌 (핵심)
- Ma et al., \"Gradient-based SMO EUV,\" IEEE TCI 2019
- Li & Li, \"Low aberration sensitivity SMO,\" IEEE TN 2017
- Zhang et al., \"EUV SMO thick mask SL-PSO,\" Optics Express 2021

## 태그
`SMO`, `EUV`, `MDPI`, `Micromachines`, `aberration-mitigation`, `patterning-fidelity`, `conjugate-gradient`, `CD-uniformity`, `MEF`, `EL`, `2nm-node`, `BEOL`, `Zernike-aberration`
