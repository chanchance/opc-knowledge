# Applicability of Global Source Mask Optimization to 22/20nm Node and Beyond

## 메타데이터
- **저자**: Kehan Tian, Moutaz Fakhry, Aasutosh Dave, Alexander Tritchkov, Jaione Tirapu-Azpiroz, Alan E. Rosenbluth, David Melville, Masaharu Sakamoto, Tadanobu Inoue, Scott Mansfield, Alexander Wei, Young Kim, Bruce Durgan, Kostas Adam, Gabriel Berger, Gandharv Bhatara, Jason Meiring, Henning Haffner, Byung-Sung Kim
- **연도**: 2011
- **게재지/학회**: Proc. SPIE 7973, Optical Microlithography XXIV, 79730C
- **DOI/URL**: https://doi.org/10.1117/12.879703
- **인용수**: 다수

## 핵심 요약
22/20nm 이하 기술 노드에서 전역 SMO(global SMO)의 적용 가능성을 분석한다. 광학 시스템의 근본적 자유도(소스 및 마스크)를 집중 최적화함으로써 비직관적 해를 생성하여 리소그래피 성능을 향상시킨다. 주요 이점으로 피치 전반의 성능 향상, 이중 패터닝 회피 가능성, 2D 패턴 우수한 성능을 입증하며, 정확한 테스트 패턴 선택이 최적화 소스의 핵심임을 강조한다.

## 주요 기여
- 22/20nm 노드 이하 전역 SMO 적용 가능성 종합 분석
- 비직관적 소스-마스크 해를 통한 리소그래피 성능 향상 입증
- 이중 패터닝 회피를 위한 SMO 활용 전략 제시
- 정확한 테스트 패턴 선택의 중요성 및 자동화 패턴 선택 방법론

## 알고리즘/수식
**전역 SMO 비용함수 (다중 패턴):**
$$F_{global}(\boldsymbol{\sigma}) = \sum_{p \in \mathcal{P}_{test}} w_p \sum_j EPE_j^2(\boldsymbol{\sigma}, m_p)$$
테스트 패턴 집합 $\mathcal{P}_{test}$에 대한 가중 EPE 합.

**피치 전반 성능 (through-pitch):**
$$F_{through-pitch}(\boldsymbol{\sigma}) = \sum_{pitch} w_{pitch} \cdot EPE^2(\boldsymbol{\sigma}; pitch)$$
다양한 피치에 대한 공통 소스 최적화.

**패턴 선택 커버리지 지표:**
$$Coverage = \frac{|\{p \in \mathcal{P}_{full} : \exists p' \in \mathcal{P}_{test}, sim(p,p') > \theta\}|}{|\mathcal{P}_{full}|}$$
테스트 패턴이 전체 패턴 공간을 대표하는 커버리지 비율.

**이중 패터닝 회피 조건:**
$$k_1 = \frac{CD \cdot NA}{\lambda} \geq 0.25 \rightarrow \text{SMO로 단일 패터닝 가능}$$

**비직관적 소스 허용 조건:**
$$\sigma_{opt} = \arg\min_\sigma F_{global}(\sigma) \quad \text{s.t.} \quad \sigma \in [0,1]^{N_{src}}$$
픽셀화 소스 공간에서 제약 없는 전역 최적화.

## OPC 툴 SMO 구현 관련성
- SKOPC 전역 SMO에서 테스트 패턴 선택 및 피치 전반 최적화 구현 시 참고
- `skopc/smo/global_smo.py`에 전역 SMO 다중 패턴 비용함수 구현
- 자동 패턴 선택은 `skopc/smo/pattern_selection.py`에 구현
- Deng et al. 2010 로직 SMO, Nagahara et al. 2010 28nm SMO와 함께 실용적 전역 SMO 계열 참고

## 참고문헌 (핵심)
- Deng et al., \"Considerations in SMO logic,\" SPIE 2010
- Nagahara et al., \"SMO 28nm logic,\" SPIE 2010
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011

## 태그
`SMO`, `SPIE`, `global-SMO`, `22nm`, `20nm`, `pattern-selection`, `through-pitch`, `double-patterning`, `process-window`, `IBM`, `Mentor`, `ASML`
