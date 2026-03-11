# Simulation-Based EUV Source and Mask Optimization

## 메타데이터
- **저자**: Tim Fühner, Andreas Erdmann, Peter Evanschitzky
- **연도**: 2008
- **게재지/학회**: Proc. SPIE 7122, Photomask Technology 2008, 71221Y
- **DOI/URL**: https://doi.org/10.1117/12.801436
- **인용수**: 다수

## 핵심 요약
EUV 리소그래피를 위한 시뮬레이션 기반 소스-마스크 최적화(SMO)를 처음으로 제안한다. 엄밀한 전자기 필드(EMF) 마스크 시뮬레이터(도파관법/RCWA)와 벡터 이미징 모델을 결합한 리소그래피 시뮬레이션으로 공정 조건을 식별한다. 단일 기준 및 다중 기준 유전 알고리즘(GA)을 적용하여 감쇠 및 교번 위상 시프트 마스크에 대한 직접 소스-마스크 공동 최적화 결과를 제시한다. Fraunhofer IISB 그룹의 초기 EUV SMO 연구.

## 주요 기여
- EUV 리소그래피에서 엄밀 EMF 마스크 시뮬레이션 기반 SMO 최초 제안
- 단일/다중 기준 유전 알고리즘 기반 EUV 소스-마스크 공동 최적화
- 도파관법(Waveguide Method)/RCWA 기반 엄밀 EUV 마스크 회절 스펙트럼 계산
- Hopkins 근사 없는 벡터 이미징 모델 적용

## 알고리즘/수식
**EUV 벡터 이미징 (Hopkins 근사 없음):**
$$I(x) = \int J(\mathbf{f}_s) \sum_\alpha \left| \int M_{EUV}(\mathbf{f}) H_\alpha(\mathbf{f}+\mathbf{f}_s) e^{i2\pi \mathbf{f} \cdot x} d\mathbf{f} \right|^2 d\mathbf{f}_s$$
소스 적분을 직접 계산 (Hopkins TCC 근사 없음).

**엄밀 EUV 마스크 회절 (도파관법):**
$$M_{EUV}(\mathbf{f}) = \mathcal{F}\left[\text{Waveguide-EMF}(m_{layout})\right](\mathbf{f})$$
다층 EUV 마스크 구조를 도파관법으로 엄밀 계산.

**단일 기준 유전 알고리즘 SMO:**
$$\min_{(\boldsymbol{\sigma}, m)} F = \sum_j EPE_j^2(\boldsymbol{\sigma}, m)$$
GA로 소스 $\boldsymbol{\sigma}$와 마스크 $m$ 동시 탐색.

**다중 기준 유전 알고리즘 (Pareto 최적화):**
$$\text{Pareto-optimal}\{F_{DOF}(\boldsymbol{\sigma},m), F_{EL}(\boldsymbol{\sigma},m), F_{CD}(\boldsymbol{\sigma},m)\}$$
DOF, EL, CD 균일성을 동시에 최적화하는 Pareto 프론트.

**EUV 소스 표현:**
$$\boldsymbol{\sigma} = \{\sigma_k\}_{k=1}^{N_{EUV}}, \quad \sigma_k \in [0,1]$$
픽셀화 EUV 소스 강도.

## OPC 툴 SMO 구현 관련성
- SKOPC EUV SMO에서 엄밀 EMF 마스크 시뮬레이션 기반 SMO의 초기 참고
- `skopc/litho/euv_vector_imaging.py`에 Hopkins 근사 없는 EUV 벡터 이미징 구현
- 다중 기준 GA SMO는 `skopc/smo/multi_objective_ga_smo.py`에 참고
- Liu et al. 2014 EUV SMO 7nm 노드와 함께 EUV SMO 발전 과정 참고

## 참고문헌 (핵심)
- Socha et al., \"Simultaneous SMO,\" SPIE 2005
- Rosenbluth et al., \"Global illumination optimization,\" SPIE 2006
- Liu et al., \"EUV SMO 7nm node,\" SPIE 2014

## 태그
`SMO`, `EUV`, `SPIE`, `simulation-based`, `genetic-algorithm`, `multi-objective`, `vector-imaging`, `RCWA`, `waveguide-method`, `EMF-simulation`, `Fraunhofer-IISB`, `Pareto`, `phase-shifting-mask`
