# Design Compliant Source Mask Optimization (SMO)

## 메타데이터
- **저자**: Robert Socha, Tejas Jhaveri, Mircea Dusa, Xiaofeng Liu, Luoqi Chen, Stephen Hsu, Zhipan Li, Andrzej J. Strojwas
- **연도**: 2010
- **게재지/학회**: Proc. SPIE 7748, Photomask and Next-Generation Lithography Mask Technology XVII, 77480T
- **DOI/URL**: https://doi.org/10.1117/12.865781
- **인용수**: 다수

## 핵심 요약
소스, 마스크, 설계를 공동 최적화하는 설계 준수(design compliant) SMO 방법을 논한다. 22nm 로직 노드 pdBRIX 로직 템플릿 및 SRAM 셀을 대상으로 접촉홀과 메탈 1 레이어에 대해 Tachyon SMO를 사용하여 소스-마스크 최적화를 수행한다. NA 1.35, FlexRay 조명이 적용된 ASML /1950 스캐너에서 40nm 하프피치 22nm 노드 패턴을 검증한다. ASML Brion Technologies.

## 주요 기여
- 설계 규칙과 SMO를 통합한 설계 준수 SMO 방법론
- 22nm 노드 pdBRIX 로직 + SRAM 접촉홀/메탈 레이어 SMO 적용
- FlexRay 조명 + Tachyon SMO 결합 실용적 SMO 흐름
- 설계-소스-마스크 공동 최적화로 설계 규칙 위반 방지

## 알고리즘/수식
**설계 준수 SMO 비용함수:**
$$F_{DC-SMO}(\boldsymbol{\sigma}, m) = F_{EPE}(\boldsymbol{\sigma}, m) + \lambda_{DRC} \cdot C_{DRC}(m)$$
EPE 충실도 항 + 설계 규칙 검사(DRC) 위반 페널티 $C_{DRC}$ 포함.

**설계 규칙 위반 페널티:**
$$C_{DRC}(m) = \sum_{r \in DRC} \max(0, \text{violation}(m; r))^2$$
각 설계 규칙 $r$에 대한 위반량의 제곱합.

**Tachyon SMO 소스 최적화:**
$$\boldsymbol{\sigma}^* = \arg\min_\boldsymbol{\sigma} \sum_{p \in \mathcal{P}} \sum_j EPE_j^2(\boldsymbol{\sigma}, m_p)$$
패턴 집합 $\mathcal{P}$ (접촉홀 + 메탈)에 대한 소스 최적화.

**FlexRay 소스 구현 제약:**
$$\sigma_{FlexRay}(\mathbf{f}) \approx \sigma_{ideal}(\mathbf{f}), \quad \|\sigma_{FlexRay} - \sigma_{ideal}\|_2 \leq \varepsilon_{FlexRay}$$
FlexRay 조명기의 소스 구현 정확도 제약.

**공정 윈도우 평가 (22nm 노드):**
$$PW = \{(dose, focus) : CD_{all} \in [CD_{nom} \pm 10\%]\}$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 설계 규칙 준수 SMO 구현 시 참고
- `skopc/smo/design_compliant_smo.py`에 DRC 페널티 포함 설계 준수 SMO 구현
- FlexRay 소스 구현 제약은 `skopc/smo/source_constraints.py`에 구현
- Tsai et al. 2011 풀칩 SMO FMO와 함께 ASML Brion Tachyon SMO 계열 참고

## 참고문헌 (핵심)
- Tsai et al., \"Full-chip SMO FMO ASML Brion,\" SPIE 2011
- Deng et al., \"Considerations in SMO logic,\" SPIE 2010
- Nagahara et al., \"SMO 28nm logic,\" SPIE 2010

## 태그
`SMO`, `SPIE`, `design-compliant`, `DRC`, `22nm`, `SRAM`, `contact-hole`, `metal-layer`, `FlexRay`, `Tachyon-SMO`, `ASML-Brion`, `pdBRIX`, `design-rules`
