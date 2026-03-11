# Exposure Latitude Aware Source and Mask Optimization for Extreme Ultraviolet Lithography

## 메타데이터
- **저자**: Lulu Zou (외)
- **연도**: 2021
- **게재지/학회**: Applied Optics, Vol. 60, No. 30, pp. 9404–9410
- **DOI/URL**: https://doi.org/10.1364/AO.440528
- **인용수**: 다수

## 핵심 요약
EUV 리소그래피의 광원 안정성 요건을 고려하여 노광 위도(exposure latitude, EL)를 명시적으로 최적화 목적함수에 통합한 노광 위도 인식(exposure latitude aware) SMO 방법을 제안한다. 기존 SMO가 단일 공칭 조건(nominal condition)에서 패턴 오차만 최소화하는 것과 달리, 도즈 변동에 대한 이미징 안정성을 목적함수에 직접 반영하여 공정 마진을 향상시킨다.

## 주요 기여
- 노광 위도(EL)를 SMO 목적함수에 직접 통합하는 새로운 비용함수 설계
- EUV 광원 도즈 변동에 대한 이미징 안정성 향상
- EL 인식 소스/마스크 동시 최적화 알고리즘 구현
- EUV 리소그래피에서 공칭 조건 최적화 대비 우수한 공정 마진 실증

## 알고리즘/수식
**노광 위도 인식 SMO 목적함수:**
$$\min_{\boldsymbol{\sigma}, m} F_{EL}(\boldsymbol{\sigma}, m) = F_{nominal}(\boldsymbol{\sigma}, m) + \lambda_{EL} \cdot F_{dose}(\boldsymbol{\sigma}, m)$$
공칭 비용함수 $F_{nominal}$과 도즈 변동 비용함수 $F_{dose}$의 가중 합.

**도즈 변동 비용함수:**
$$F_{dose} = \sum_j \left(\frac{\partial EPE_j}{\partial D}\right)^2$$
도즈 $D$에 대한 EPE 민감도를 최소화하여 도즈 변동에 강인한 소스/마스크 설계.

**노광 위도 정의:**
$$EL = \frac{D_{max} - D_{min}}{D_{nominal}} \times 100\%$$
허용 CD 변동 범위 내에서 도즈 변동 허용 범위 $[D_{min}, D_{max}]$.

**그래디언트 기반 최적화:**
$$\frac{\partial F_{EL}}{\partial \sigma_k} = \frac{\partial F_{nominal}}{\partial \sigma_k} + \lambda_{EL} \frac{\partial F_{dose}}{\partial \sigma_k}$$
소스 그래디언트에 도즈 민감도 항 추가.

$$\frac{\partial F_{EL}}{\partial m_j} = \frac{\partial F_{nominal}}{\partial m_j} + \lambda_{EL} \frac{\partial F_{dose}}{\partial m_j}$$
마스크 그래디언트도 동일하게 확장.

**EUV 이미징 모델:**
$$I(x; D) = D \cdot \sum_k \sigma_k |h_k * m|^2(x)$$
도즈 $D$ 스케일링을 포함한 aerial image 모델.

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 노광 위도 인식 비용함수 구현 시 직접 참고
- `skopc/smo/el_aware_smo.py` 구현으로 도즈 변동에 강인한 EUV SMO 가능
- 도즈 민감도 그래디언트는 기존 그래디언트 기반 SMO에 항 추가로 구현 가능
- 공정 마진 최적화 SMO 비용함수 설계 참고 (EL + DOF 복합 목적함수)

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Ma et al., "Gradient-based EUV SMO," IEEE TCI 2019
- Jia & Lam, "Pixelated SMO process robustness," Optics Express 2011
- Hashimoto et al., "Robust SMO," SPIE 2013

## 태그
`SMO`, `Applied-Optics`, `EUV-lithography`, `exposure-latitude`, `dose-sensitivity`, `process-window`, `robust-SMO`, `gradient-based`, `dose-variation`, `imaging-stability`
