# Efficient Source Mask Optimization Using Multipole Source Representation

## 메타데이터
- **저자**: Chaoxing Yang, Sikun Li, Xiangzhao Wang
- **연도**: 2014
- **게재지/학회**: Journal of Micro/Nanolithography, MEMS, and MOEMS, Vol. 13, No. 4, 043001
- **DOI/URL**: https://doi.org/10.1117/1.JMM.13.4.043001
- **인용수**: 확인 필요

## 핵심 요약
유전 알고리즘 기반 SMO(GA-SMO)의 계산 효율을 높이기 위해 다극 소스 표현(multipole source representation)을 제안한다. 픽셀 충진율(Pupil Filling Ratio, PFR)이 작은 프리폼 조명 소스를 원형 극(circular poles) 그룹으로 기술하여 탐색 변수 수를 대폭 줄이고 GA-SMO의 수렴 속도와 효율을 향상시킨다.

## 주요 기여
- 다극 소스 표현(multipole source representation)으로 GA-SMO 가속
- 원형 극 기반 프리폼 소스 매개변수화로 탐색 변수 감소
- 낮은 픽셀 충진율(PFR) 소스에서 특히 효과적
- GA 기반 소스 최적화의 계산 효율 향상

## 알고리즘/수식
**다극 소스 표현:**
$$\boldsymbol{\sigma}(\mathbf{f}) = \sum_{p=1}^{N_{poles}} A_p \cdot \text{circ}\left(\frac{|\mathbf{f} - \mathbf{c}_p|}{r_p}\right)$$
$N_{poles}$개의 원형 극으로 소스 표현: 중심 $\mathbf{c}_p$, 반경 $r_p$, 강도 $A_p$.

**GA 탐색 변수 (다극 표현):**
$$\boldsymbol{\theta} = \{A_p, \mathbf{c}_p, r_p\}_{p=1}^{N_{poles}}, \quad |\boldsymbol{\theta}| = 4N_{poles}$$
픽셀화 소스($N_{src}$ 변수) 대비 대폭 감소된 $4N_{poles}$ 변수.

**SMO 비용함수 (GA):**
$$F_{GA}(\boldsymbol{\theta}, m) = \sum_j EPE_j^2(\boldsymbol{\sigma}(\boldsymbol{\theta}), m)$$

**픽셀 충진율 (PFR):**
$$PFR = \frac{\sum_k \mathbf{1}[\sigma_k > 0]}{N_{src}}$$
소스 퓨필 내 활성 픽셀 비율 — 낮을수록 다극 표현이 효과적.

**GA 진화 연산:**
실수 코딩 GA(RCGA)로 다극 소스 매개변수 $\boldsymbol{\theta}$ 진화:
$$\boldsymbol{\theta}^{(t+1)} = \text{GA-evolve}(\boldsymbol{\theta}^{(t)}, F_{GA})$$

## OPC 툴 SMO 구현 관련성
- SKOPC 프리폼 소스 GA-SMO에서 다극 소스 매개변수화 구현 시 참고
- `skopc/smo/multipole_source_smo.py`에 다극 소스 표현 GA-SMO 구현
- Yang et al. 2013 RCGA SMO와 함께 GA 기반 SMO 계열로 참고
- 낮은 PFR 소스(쿼드루폴, 다이폴 등)에서 픽셀화 소스 대안으로 활용

## 참고문헌 (핵심)
- Yang et al., \"Genetic algorithm SMO,\" SPIE 2013
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011
- Wu et al., \"Zernike source representation SMO,\" Optics Express 2014

## 태그
`SMO`, `JMM`, `SPIE`, `multipole-source`, `source-representation`, `genetic-algorithm`, `GA-SMO`, `freeform-source`, `PFR`, `parametric-source`, `computational-efficiency`
