# Robust Source and Polarization Joint Optimization for Thick-Mask Lithography Imaging

## 메타데이터
- **저자**: Shengen Zhang, Xu Ma, Gonzalo R. Arce
- **연도**: 2024
- **게재지/학회**: Journal of Micro/Nanopatterning, Materials, and Metrology, Vol. 23, No. 4, 043201
- **DOI/URL**: https://doi.org/10.1117/1.JMM.23.4.043201
- **인용수**: 확인 필요

## 핵심 요약
소스 강도 분포와 편광 각도를 동시에 최적화하는 소스-편광 공동 최적화(SPO, Source and Polarization joint Optimization) 방법을 개발한다. 두꺼운 마스크(thick mask)의 3D 회절 효과를 엄밀 시뮬레이터로 모델링하고, 초점/디포커스 이미징 평면과 노광 변동을 모두 고려한 강인(robust) SPO 프레임워크를 구축하여 공정 변동 하에서 리소그래피 이미지 품질을 향상시킨다.

## 주요 기여
- 소스-편광 공동 최적화(SPO) 프레임워크 개발
- 3D 엄밀 회절 시뮬레이터 기반 두꺼운 마스크 효과 모델링
- 초점/디포커스 + 노광 변동 강인성 SPO 구현
- 임계치수(CD) 회절 해상도 한계 근방에서의 두꺼운 마스크 영향 보정

## 알고리즘/수식
**SPO 목적함수 (강인):**
$$F_{SPO}(\boldsymbol{\sigma}, \boldsymbol{\phi}) = \sum_{\delta \in \Delta} w_\delta \sum_j \left(I_j(\boldsymbol{\sigma}, \boldsymbol{\phi}; \delta) - I_{target,j}\right)^2$$
공정 변동 집합 $\Delta$ (초점/노광 변동)에 대한 가중 오차 합.

**벡터 이미징 모델 (편광 포함 두꺼운 마스크):**
$$I(x; \boldsymbol{\sigma}, \boldsymbol{\phi}) = \sum_k \sigma_k \sum_{\alpha \in \{x,y,z\}} \left| \sum_{\mathbf{f}} M_{3D}(\mathbf{f}) H_\alpha(\mathbf{f}; \phi_k) e^{i2\pi \mathbf{f} \cdot x} \right|^2$$
3D 마스크 회절 스펙트럼 $M_{3D}$와 편광 의존 pupil $H_\alpha$를 포함.

**편광 각도 그래디언트:**
$$\frac{\partial F_{SPO}}{\partial \phi_k} = \sum_j \frac{\partial F}{\partial I_j} \cdot \frac{\partial I_j}{\partial \phi_k}$$

**소스 강도 그래디언트:**
$$\frac{\partial F_{SPO}}{\partial \sigma_k} = \sum_j \frac{\partial F}{\partial I_j} \cdot \frac{\partial I_j}{\partial \sigma_k}$$

**두꺼운 마스크 3D 회절 모델:**
$$M_{3D}(\mathbf{f}) = \mathcal{F}\left[\text{RCWA}(m_{layout})\right](\mathbf{f})$$
RCWA(Rigorous Coupled-Wave Analysis) 기반 3D 마스크 회절 스펙트럼.

## OPC 툴 SMO 구현 관련성
- SKOPC 두꺼운 마스크 EUV SMO에서 편광 공동 최적화 구현 시 참고
- `skopc/smo/spo_thick_mask.py`에 SPO 프레임워크 구현
- 3D 마스크 효과 포함 벡터 이미징 모델은 `skopc/litho/vector_imaging_3d.py`에 활용
- Zhang et al. 2021 EUV SMO thick mask SL-PSO와 함께 두꺼운 마스크 SMO 계열 참고

## 참고문헌 (핵심)
- Ma et al., \"Gradient-based joint SPMO,\" JM3 2015
- Zhang et al., \"EUV SMO thick mask SL-PSO,\" Optics Express 2021
- Li et al., \"Robust SMO mask topography Zernike,\" Optics Express 2014

## 태그
`SMO`, `JMM`, `SPIE`, `polarization`, `SPO`, `thick-mask`, `robust-SMO`, `3D-mask`, `RCWA`, `vector-imaging`, `source-polarization-coopt`, `process-window`
