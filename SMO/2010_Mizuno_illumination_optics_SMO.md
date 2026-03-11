# Illumination Optics for Source-Mask Optimization

## 메타데이터
- **저자**: Yasushi Mizuno, Tomoyuki Matsuyama, Soichi Owa, Osamu Tanitsu, Naonori Kita, Masahiko Okumura
- **연도**: 2010
- **게재지/학회**: Proc. SPIE 7640, Optical Microlithography XXIII, 76401I
- **DOI/URL**: https://doi.org/10.1117/12.846476
- **인용수**: 확인 필요

## 핵심 요약
SMO를 위한 조명 광학계의 역할과 구성을 분석한다. SMO 툴이 자유형(freeform) 모드와 제약(constrained) 모드로 운영되며, 자유형 모드에서는 마스크 파라미터에 연속 진폭 투과율과 위상 분포를 포함하는 더 큰 자유도를 허용하는 반면 제약 모드에서는 제한된 마스크 파라미터만 허용한다. Nikon Corp.

## 주요 기여
- SMO를 위한 조명 광학계(illumination optics)의 역할 분석
- SMO 자유형 모드와 제약 모드의 비교 분석
- Nikon 스캐너에서 SMO 소스 구현 방법론
- 조명 파라미터와 마스크 자유도의 상호 관계 분석

## 알고리즘/수식
**자유형 SMO 모드:**
$$\boldsymbol{\sigma}_{free} \in [0,1]^{N_{src}}, \quad m_{free} \in \mathbb{C}^{N_{mask}}$$
픽셀화 소스 + 연속 복소 마스크 진폭/위상.

**제약 SMO 모드:**
$$\boldsymbol{\sigma}_{constrained} = f(\boldsymbol{\theta}_{illum}), \quad m_{constrained} \in \{0, 1\}$$
조명 파라미터 $\boldsymbol{\theta}_{illum}$ (NA, sigma_inner/outer, 형상)로 제약된 소스.

**조명 자유도 비교:**
$$DOF_{freeform} > DOF_{constrained}$$
$$\Delta F = F_{freeform}^* - F_{constrained}^* \leq 0$$
자유형 모드가 제약 모드보다 낮은 비용함수 달성.

**스캐너 소스 구현 제약:**
$$\sigma_{scanner}(\mathbf{f}) = \Pi_{FlexRay}(\sigma_{ideal}(\mathbf{f}))$$
FlexRay 조명기를 통한 이상적 소스 구현.

**조명 파라미터 최적화:**
$$\boldsymbol{\theta}^* = \arg\min_{\boldsymbol{\theta}} F_{SMO}(\boldsymbol{\sigma}(\boldsymbol{\theta}), m^*)$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 조명 광학계 제약 모델링 시 자유형/제약 모드 구분 참고
- `skopc/smo/illumination_constraint.py`에 스캐너 조명 제약 구현
- Aoyama et al. 2013 현실적 소스 형상, Matsuyama et al. 2009 ArF 스캐너와 함께 Nikon 스캐너 SMO 계열 참고

## 참고문헌 (핵심)
- Matsuyama et al., \"SMO ArF scanner,\" SPIE 2009
- Nakashima et al., \"Feasibility SMO 45nm,\" SPIE 2009
- Aoyama et al., \"Realistic source shape SMO,\" JM3 2013

## 태그
`SMO`, `SPIE`, `illumination-optics`, `freeform-mode`, `constrained-mode`, `Nikon`, `scanner`, `FlexRay`, `source-constraints`, `optical-system`, `ArF-immersion`
