# Source Mask Optimization Based on Design Pattern Library at 7nm Technology Node

## 메타데이터
- **저자**: Xiaojing Su, Lisong Dong, Yayi Wei, Tianyang Gai, Yajuan Su, Rui Chen
- **연도**: 2021
- **게재지/학회**: Proc. SPIE 11614, Design-Process-Technology Co-optimization XV, 116140P
- **DOI/URL**: https://doi.org/10.1117/12.2584716
- **인용수**: 확인 필요

## 핵심 요약
7nm 기술 노드에서 설계 패턴 라이브러리(design pattern library)를 기반으로 한 SMO 방법을 개발한다. 설계 패턴 라이브러리로 반복적인 SMO 변화를 관리하고 비교하여 프리폼 소스 최적화의 효율성을 높이며, 7nm 임계 레이어에서의 SMO 적용에 대한 방법론을 제시한다.

## 주요 기여
- 설계 패턴 라이브러리 기반 SMO 관리 체계 개발
- 7nm 임계 레이어에서의 SMO 적용 방법론
- 반복 SMO 변화 추적 및 비교를 위한 패턴 라이브러리 활용
- 프리폼 소스 최적화와 패턴 라이브러리의 통합

## 알고리즘/수식
**패턴 라이브러리 기반 SMO:**
$$\boldsymbol{\sigma}^* = \arg\min_{\boldsymbol{\sigma}} \sum_{p \in \mathcal{L}_{design}} w_p \sum_j EPE_j^2(\boldsymbol{\sigma}, m_p)$$
설계 패턴 라이브러리 $\mathcal{L}_{design}$에서 소스 최적화.

**패턴 유사도 기반 클러스터링:**
$$\mathcal{L}_{critical} = \{p \in \mathcal{L}_{design} : \text{EPE}_{nominal}(p) > EPE_{th}\}$$
공칭 EPE 임계값 초과 패턴을 임계 패턴으로 분류.

**라이브러리 기반 커버리지 평가:**
$$Coverage(\mathcal{L}_{critical}) = \frac{|\{p_{full} : \exists p_{lib} \in \mathcal{L}_{critical}, sim(p_{full}, p_{lib}) > \theta\}|}{|\mathcal{P}_{full}|}$$

**반복 SMO 비교 지표:**
$$\Delta F_{iter} = F_{SMO}(\boldsymbol{\sigma}^{(t+1)}, m) - F_{SMO}(\boldsymbol{\sigma}^{(t)}, m)$$
반복 간 비용함수 변화량으로 수렴 판단.

## OPC 툴 SMO 구현 관련성
- SKOPC 7nm 임계 레이어 SMO에서 설계 패턴 라이브러리 기반 패턴 선택 참고
- `skopc/smo/pattern_library_smo.py`에 설계 패턴 라이브러리 기반 SMO 구현
- Tian et al. 2011 전역 SMO 패턴 선택, Liao et al. 2020 풀칩 임계 패턴 선택과 함께 참고

## 참고문헌 (핵심)
- Tian et al., \"Applicability global SMO 22nm,\" SPIE 2011
- Liao et al., \"Critical pattern selection fullchip SMO,\" Optics Express 2020
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011

## 태그
`SMO`, `SPIE`, `7nm`, `design-pattern-library`, `pattern-library`, `pattern-selection`, `freeform-source`, `critical-layer`, `DTCO`, `coverage`
