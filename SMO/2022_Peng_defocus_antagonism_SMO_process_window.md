# Source and Mask Optimizing with a Defocus Antagonism for Process Window Enhancement

## 메타데이터
- **저자**: Fei Peng, Yiduo Xu, Yi Song, Chengqun Gui, Yan Zhao
- **연도**: 2022
- **게재지/학회**: Optics Express, Vol. 30, No. 20, pp. 36429–36445
- **DOI/URL**: https://doi.org/10.1364/OE.469275
- **인용수**: 확인 필요

## 핵심 요약
소스, 마스크, 디포커스를 동시에 최적화 변수로 사용하는 디포커스 생성적 대립(Defocus Generative and Adversarial SMO, DGASMO) 방법을 제안한다. 패널티 항이 디포커스를 외부로 밀어내는 동시에 패턴 충실도가 내부로 당기는 대립(antagonism) 과정에서 최적 소스와 마스크를 탐색하여 DOF를 제어한다. Adam 알고리즘으로 역 이미징 프레임워크를 가속하며 85nm 노드에서 PW/DOF 최대 44% 향상을 실증한다.

## 주요 기여
- 디포커스를 최적화 변수로 포함하는 DGASMO 프레임워크 제안
- 디포커스 패널티와 패턴 충실도의 대립 메커니즘으로 DOF 직접 제어
- Adam 알고리즘 기반 역 이미징 최적화 가속
- 85nm 노드: PW 29.12%, DOF 44.09% 향상 / 55nm 노드: PW 190.2%, DOF 118.42% 향상

## 알고리즘/수식
**DGASMO 목적함수 (디포커스 대립):**
$$\min_{\boldsymbol{\sigma}, m} \max_{\delta f} \mathcal{L}(\boldsymbol{\sigma}, m, \delta f) = F_{EPE}(\boldsymbol{\sigma}, m, \delta f) - \lambda_{df} |\delta f|^2$$
소스/마스크는 EPE 최소화, 디포커스는 크기 최대화 → 대립 구조.

**DGASMO 등가 형식:**
$$\min_{\boldsymbol{\sigma}, m} F_{total} = F_{EPE,nominal} + F_{EPE,defocus} + \lambda_{df} F_{df}$$
$$F_{df} = \max(0, \delta f_{target} - |\delta f_{opt}|)^2$$
디포커스 항이 목표 디포커스보다 작아지면 패널티 부과.

**디포커스 포함 이미징 모델:**
$$I(x; \delta f) = \sum_k \sigma_k |h_k(\cdot; \delta f) * m|^2(x)$$
$$h_k(x; \delta f) = \mathcal{F}^{-1}\left[H_k(f) \cdot \exp\left(i \frac{\pi \delta f}{\lambda} (f^2+g^2)\right)\right]$$

**Adam 기반 소스/마스크 업데이트:**
$$\boldsymbol{\sigma}^{(t+1)} \leftarrow \text{Adam}\left(\boldsymbol{\sigma}^{(t)}, \nabla_\sigma F_{total}\right)$$
$$m^{(t+1)} \leftarrow \text{Adam}\left(m^{(t)}, \nabla_m F_{total}\right)$$

**대립 메커니즘:**
- 패널티 항: 디포커스 $\delta f$를 외부(더 큰 디포커스)로 밀어냄
- 패턴 충실도 항: 이미징 왜곡 방지를 위해 디포커스 제한
- 균형점: 최대 DOF 달성

**성능 결과:**
- 85nm (EL=15%): PW +29.12%, DOF +44.09%
- 55nm (EL=2%): PW +190.2%, DOF +118.42%

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 DOF 직접 최대화 전략으로 DGASMO 구현 참고
- `skopc/smo/dgasmo.py`에 디포커스 대립 SMO 구현
- Adam 기반 소스/마스크 업데이트는 `skopc/smo/adaptive_smo.py`와 결합 가능
- 디포커스를 최적화 변수로 포함하는 접근은 공정 마진 최대화 SMO의 새로운 패러다임

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Shen et al., "Adaptive gradient SMO," Chinese Optics Letters 2019
- Xu et al., "Global NILS control SMO," Applied Optics 2023

## 태그
`SMO`, `Optics-Express`, `DGASMO`, `defocus-antagonism`, `process-window`, `DOF`, `Adam`, `generative-adversarial`, `depth-of-focus`, `exposure-latitude`, `inverse-imaging`
