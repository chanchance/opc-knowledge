# Mutual Source, Mask and Projector Pupil Optimization

## 메타데이터
- **저자**: Tim Fühner, Peter Evanschitzky, Andreas Erdmann
- **연도**: 2012
- **게재지/학회**: Proc. SPIE 8326, Optical Microlithography XXV, 83260I
- **DOI/URL**: https://doi.org/10.1117/12.916529
- **인용수**: 확인 필요

## 핵심 요약
소스, 마스크, 투영 렌즈 퓨필을 동시에 최적화하는 상호 소스-마스크-퓨필 최적화(SMPO) 절차를 제시한다. 다양한 라인/스페이스 구성의 공통 공정 윈도우 최대화를 목표로 하며, 픽셀화 소스, 주 패턴 크기, SRAF 구성을 함께 최적화한다. Fraunhofer IISB 그룹의 연구.

## 주요 기여
- 소스-마스크-퓨필 3변수 공동 최적화(SMPO) 절차 제시
- 다양한 라인/스페이스 패턴의 공통 공정 윈도우 최대화
- 픽셀화 소스 + 주 패턴 크기 + SRAF 동시 최적화
- 투영 렌즈 퓨필 위상(aberration) 포함 최적화

## 알고리즘/수식
**SMPO 3변수 비용함수:**
$$F(\boldsymbol{\sigma}, m, \boldsymbol{\Psi}) = \sum_{p \in \mathcal{P}} w_p \sum_j EPE_j^2(\boldsymbol{\sigma}, m_p, \boldsymbol{\Psi})$$
소스 $\boldsymbol{\sigma}$, 마스크 $m$, 퓨필 위상 $\boldsymbol{\Psi}$에 대한 패턴 집합 $\mathcal{P}$ EPE 합.

**퓨필 위상 (Zernike 매개변수화):**
$$\Psi(\mathbf{f}) = \sum_n a_n Z_n(\mathbf{f})$$
Zernike 다항식 계수 $a_n$으로 퓨필 위상 매개변수화.

**공통 공정 윈도우 최대화:**
$$\max_{\boldsymbol{\sigma}, m, \boldsymbol{\Psi}} PW_{common}(\boldsymbol{\sigma}, m, \boldsymbol{\Psi})$$
$$PW_{common} = \bigcap_{p \in \mathcal{P}} PW_p(\boldsymbol{\sigma}, m_p, \boldsymbol{\Psi})$$

**소스 그래디언트:**
$$\frac{\partial F}{\partial \sigma_k} = \sum_p \sum_j w_p \cdot 2EPE_j \cdot \frac{\partial EPE_j}{\partial \sigma_k}$$

**퓨필 위상 그래디언트:**
$$\frac{\partial F}{\partial a_n} = \sum_p \sum_j w_p \cdot 2EPE_j \cdot \frac{\partial EPE_j}{\partial a_n}$$

**이미징 모델 (퓨필 포함):**
$$I(x; \boldsymbol{\sigma}, m, \boldsymbol{\Psi}) = \sum_k \sigma_k \left| \int M(\mathbf{f}) H_k(\mathbf{f}) e^{i\Psi(\mathbf{f})} e^{i2\pi \mathbf{f} \cdot x} d\mathbf{f} \right|^2$$

## OPC 툴 SMO 구현 관련성
- SKOPC 3변수 SMPO 구현 시 소스-마스크-퓨필 동시 최적화 참고
- `skopc/smo/smpo_source_mask_pupil.py`에 Zernike 퓨필 포함 SMPO 구현
- Li & Lam 2014 SPIE SMPO와 함께 소스-마스크-퓨필 3변수 최적화 계열 참고
- 투영 렌즈 수차 포함 강인 SMO의 기초 프레임워크로 활용

## 참고문헌 (핵심)
- Li & Lam, \"Joint SMO pupil,\" SPIE 2014
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011
- Tsai et al., \"Fullchip SMO ASML Brion,\" SPIE 2011

## 태그
`SMO`, `SPIE`, `SMPO`, `source-mask-pupil`, `3-variable-optimization`, `Zernike-pupil`, `process-window`, `SRAF`, `Fraunhofer-IISB`, `aberration`, `common-process-window`
