# Gradient-Based Source Mask and Polarization Optimization with the Hybrid Hopkins–Abbe Model

## 메타데이터
- **저자**: Ming Ding, Zhiyuan Niu, Fang Zhang, Linglin Zhu, Weijie Shi, Aijun Zeng, Huijie Huang
- **연도**: 2020
- **게재지/학회**: Journal of Micro/Nanolithography, MEMS, and MOEMS, Vol. 19, 033201
- **DOI/URL**: https://doi.org/10.1117/1.JMM.19.3.033201
- **인용수**: 확인 필요

## 핵심 요약
28nm 이하 노드에서 SMO의 확장으로 편광 변수를 추가한 소스-마스크-편광 최적화(SMPO)를 하이브리드 Hopkins-Abbe 이미징 모델로 구현한다. 기존 Hopkins 이론의 일정 마스크 회절 효율 가정 한계를 하이브리드 Hopkins-Abbe 방법으로 극복하고, 그래디언트 하강법으로 소스, 마스크, 편광을 동시 최적화하여 리소그래피 제조 가능성을 향상시킨다.

## 주요 기여
- 하이브리드 Hopkins-Abbe 이미징 모델 기반 그래디언트 SMPO 개발
- 편광 변수 추가로 SMO 해 공간 확장
- 기존 Hopkins 이론의 일정 회절 효율 가정 한계 극복
- 28nm 이하 노드에서 SMPO의 제조 가능성 향상 입증

## 알고리즘/수식
**하이브리드 Hopkins-Abbe 이미징 모델:**
$$I(x) = \underbrace{\sum_{k=1}^{N_{SOCS}} |\lambda_k^{1/2} h_k * m|^2}_{\text{Hopkins 항 (저주파)}} + \underbrace{\sum_k \sigma_k \sum_\alpha |H_{k,\alpha} \cdot M|^2}_{\text{Abbe 항 (고주파/경사각)}}$$
Hopkins SOCS 항과 Abbe 직접 항의 하이브리드 합산.

**SMPO 3변수 비용함수:**
$$F_{SMPO}(\boldsymbol{\sigma}, m, \boldsymbol{\phi}) = \sum_j EPE_j^2(\boldsymbol{\sigma}, m, \boldsymbol{\phi}) + \lambda_{reg} \Omega(m)$$
소스 $\boldsymbol{\sigma}$, 마스크 $m$, 편광 각도 $\boldsymbol{\phi}$ 동시 최적화.

**편광 그래디언트:**
$$\frac{\partial F_{SMPO}}{\partial \phi_k} = \sum_j 2EPE_j \cdot \frac{\partial EPE_j}{\partial I_j} \cdot \frac{\partial I_j}{\partial \phi_k}$$

**하이브리드 Hopkins-Abbe 편광 의존 이미지:**
$$I(x; \phi_k) = I_{Hopkins}(x) + \sum_k \sigma_k \sum_\alpha |H_{k,\alpha}(\phi_k) \cdot M|^2(x)$$

**소스 그래디언트 (하이브리드 모델):**
$$\frac{\partial F}{\partial \sigma_k} = \sum_j 2EPE_j \frac{\partial EPE_j}{\partial I_j} \left(\sum_\alpha |[H_{k,\alpha} \cdot M] * \delta_{x_j}|^2\right)$$

## OPC 툴 SMO 구현 관련성
- SKOPC 하이브리드 Hopkins-Abbe 이미징 기반 SMPO 구현 시 핵심 참고
- `skopc/litho/hybrid_hopkins_abbe.py`에 하이브리드 이미징 모델 구현
- `skopc/smo/smpo_hybrid.py`에 하이브리드 SMPO 구현
- Ma et al. 2015 SPMO, Zhang et al. 2024 강인 SPO thick mask와 함께 편광 최적화 계열 참고

## 참고문헌 (핵심)
- Ma et al., \"Gradient-based joint SPMO,\" JM3 2015
- Zhang et al., \"Robust SPO thick mask,\" JMM 2024
- Hansen, \"Source mask polarization optimization,\" JM3 2011

## 태그
`SMO`, `JMM`, `SPIE`, `SMPO`, `polarization`, `hybrid-Hopkins-Abbe`, `gradient-based`, `28nm`, `manufacturability`, `source-mask-polarization`, `Abbe-model`
