# Lithographic Source and Mask Optimization With Low Aberration Sensitivity

## 메타데이터
- **저자**: T. Li, Y. Li
- **연도**: 2017
- **게재지/학회**: IEEE Transactions on Nanotechnology, Vol. 16, No. 6, pp. 1099–1105
- **DOI/URL**: https://doi.org/10.1109/TNANO.2017.2752158
- **인용수**: 확인 필요

## 핵심 요약
불확실한 렌즈 수차에 대한 리소그래피 성능의 강인성을 향상시키기 위한 저수차 민감도 SMO(LASSMO, Low Aberration Sensitivity SMO) 방법을 제안한다. 현재 SMO 비용함수에 수차 민감도 페널티 항을 추가하고 정규화 확률적 경사 하강(NSGD) 알고리즘으로 반복 최적화 프레임워크를 구축한다. 45nm CD 타겟 패턴에서 구면 수차(spherical)와 코마(coma) 수차에 대한 효과를 검증한다.

## 주요 기여
- 저수차 민감도 SMO(LASSMO) 방법 제안
- 수차 민감도 페널티 항으로 확장된 SMO 비용함수 설계
- 정규화 확률적 경사 하강(NSGD) 알고리즘 기반 반복 최적화
- 구면 수차(Z9) 및 코마(Z7/Z8) 수차 민감도 저감 검증

## 알고리즘/수식
**LASSMO 비용함수:**
$$F_{LASSMO}(\boldsymbol{\sigma}, m) = F_{EPE}(\boldsymbol{\sigma}, m) + \lambda_{aber} \sum_n S_n^2(\boldsymbol{\sigma}, m)$$
EPE 항에 수차 민감도 페널티 $S_n^2$ 추가.

**수차 민감도 페널티:**
$$S_n(\boldsymbol{\sigma}, m) = \frac{\partial EPE}{\partial a_n}\bigg|_{a_n=0}$$
Zernike 수차 계수 $a_n$에 대한 EPE 편미분 — 수차 민감도.

**NSGD (Normalized Stochastic Gradient Descent) 업데이트:**
$$\boldsymbol{\sigma}^{(t+1)} = \boldsymbol{\sigma}^{(t)} - \eta \cdot \frac{\nabla_\sigma F_{LASSMO}}{\|\nabla_\sigma F_{LASSMO}\|}$$
$$m^{(t+1)} = m^{(t)} - \eta \cdot \frac{\nabla_m F_{LASSMO}}{\|\nabla_m F_{LASSMO}\|}$$
정규화된 그래디언트 방향으로 업데이트.

**수차 영향 이미징 모델:**
$$I(x; \boldsymbol{\sigma}, m, \boldsymbol{a}) = \sum_k \sigma_k \left|\int M(\mathbf{f}) H_k(\mathbf{f}) e^{i\sum_n a_n Z_n(\mathbf{f})} e^{i2\pi \mathbf{f} \cdot x} d\mathbf{f}\right|^2$$
Zernike 수차 계수 $\boldsymbol{a} = \{a_n\}$ 포함 이미징 모델.

**수차 민감도 그래디언트:**
$$\frac{\partial S_n}{\partial \sigma_k} = \frac{\partial^2 EPE}{\partial a_n \partial \sigma_k}\bigg|_{a_n=0}$$
혼합 편미분으로 수차-소스 결합 민감도 계산.

## OPC 툴 SMO 구현 관련성
- SKOPC 수차 강인 SMO 구현 시 LASSMO 수차 민감도 페널티 참고
- `skopc/smo/aberration_robust_smo.py`에 수차 민감도 페널티 포함 SMO 구현
- Zernike 수차 모델은 `skopc/litho/aberration_model.py`에 구현
- Wu et al. 2014 Zernike 소스 표현 SMO와 함께 수차 관련 SMO 계열 참고

## 참고문헌 (핵심)
- Wu et al., \"Zernike source representation SMO,\" Optics Express 2014
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011
- Li & Lam, \"Joint source mask pupil optimization,\" SPIE 2014

## 태그
`SMO`, `IEEE-TN`, `aberration-sensitivity`, `LASSMO`, `low-aberration`, `NSGD`, `Zernike-aberration`, `robust-SMO`, `spherical-aberration`, `coma`, `stochastic-gradient`, `45nm`
