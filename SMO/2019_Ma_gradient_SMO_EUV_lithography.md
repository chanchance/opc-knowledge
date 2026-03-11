# Gradient-Based Source Mask Optimization for Extreme Ultraviolet Lithography

## 메타데이터
- **저자**: Xu Ma, Zhiqiang Wang, Xianhe Chen, Yanqiu Li, Gonzalo R. Arce
- **연도**: 2019 (온라인 게재 2018)
- **게재지/학회**: IEEE Transactions on Computational Imaging, Vol. 5, No. 1, pp. 120–135
- **DOI/URL**: https://doi.org/10.1109/TCI.2018.2880342
- **인용수**: 다수 (EUV SMO 분야 핵심 논문)

## 핵심 요약
EUV 리소그래피를 위한 두 가지 모델 기반 SMO 프레임워크(파라메트릭 SMO와 픽셀화 SMO)를 개발한다. 광학 근접 효과, 플레어, 포토레지스트 효과를 근사하는 비선형 이미징 모델을 기반으로, 파라메트릭 SMO에서는 소스 패턴을 기하학적 파라미터로 정의하고, 픽셀화 SMO에서는 소스를 그리드 패턴으로 표현한다. EUV 특유의 3D 마스크 효과와 비텔레센트리시티를 고려한 최초의 체계적 그래디언트 기반 EUV-SMO 프레임워크이다.

## 주요 기여
- EUV용 파라메트릭 SMO와 픽셀화 SMO 두 가지 프레임워크 체계화
- EUV 3D 마스크 효과(그림자 효과, 비텔레센트리시티)를 포함한 비선형 이미징 모델
- 플레어 및 포토레지스트 효과를 해석적 폐형식으로 포함한 통합 모델
- 193nm 대비 EUV에서 SMO 적용 시 추가로 고려해야 할 물리 효과 분석

## 알고리즘/수식
**EUV 비선형 이미징 모델:**
$$I(x) = \sum_k \sigma_k |h_k^{EUV} * m(x)|^2 + I_{flare}$$
여기서 $h_k^{EUV}$는 EUV 시스템의 부분 코히어런트 커널 (3D 마스크 효과 포함).

**파라메트릭 소스 SMO:**
소스 패턴을 기하학적 파라미터 집합 $\theta = [\theta_1, ..., \theta_p]$로 표현:
$$\min_{\theta, m} F(I(x;\theta,m)) \quad \text{s.t.} \quad 0 \leq \sigma(\theta) \leq 1$$

**픽셀화 SMO 그래디언트:**
$$\frac{\partial F}{\partial \sigma_k} = \sum_x \frac{\partial F}{\partial I(x)} \cdot |h_k^{EUV} * m(x)|^2$$
$$\frac{\partial F}{\partial m(r)} = 2\text{Re}\left[\sum_k \sigma_k (h_k^{EUV} * m)^*(x) \cdot h_k^{EUV}(x-r)\right] \cdot \frac{\partial F}{\partial I}$$

**목적함수 (EPE 기반):**
$$F = \sum_{j} \max(0, |EPE_j| - \epsilon)^2 + \lambda_s R_s(\sigma) + \lambda_m R_m(m)$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO 모듈의 EUV 확장 구현 시 직접 참조 가능
- EUV 3D 마스크 모델을 TorchLitho와 연동하는 방법의 이론적 기반
- 파라메트릭 소스(annular, quasar, dipole 등)와 픽셀화 소스 양쪽 구현 방법 제시
- `skopc/smo/euv_smo.py` 구현 시 비선형 이미징 모델의 그래디언트 도출 참조

## 참고문헌 (핵심)
- Peng et al., "Gradient-based source and mask optimization in optical lithography," IEEE TIP 2011
- Rosenbluth et al., "Optimum mask and source patterns," JM3 2002
- Ma & Arce, "Generalized inverse lithography methods," Optics Express 2007

## 태그
`SMO`, `IEEE`, `EUV`, `gradient-based`, `parametric-SMO`, `pixelated-SMO`, `3D-mask-effect`, `flare`, `nonlinear-imaging-model`, `EUV-lithography`
