# Considerations in Source-Mask Optimization for Logic Applications

## 메타데이터
- **저자**: Yunfei Deng, Yi Zou, Kenji Yoshimoto, Yuansheng Ma, Cyrus E. Tabery, Jongwook Kye, Luigi Capodieci, Harry J. Levinson
- **연도**: 2010
- **게재지/학회**: Proc. SPIE 7640, Optical Microlithography XXIII, 76401J
- **DOI/URL**: https://doi.org/10.1117/12.848865
- **인용수**: 다수

## 핵심 요약
랜덤 로직 응용에서 전역 소스 최적화에 SMO 방법을 적용할 때의 중요한 고려 사항을 분석한다. SMO는 현실적이고 실용적인 비용함수와 정확한 공정 데이터 모델링이 필요하며, 소스 포인트 영향 인자(Source Point Impact Factor, SPIF) 개념을 도입하여 최적화 출력이 SMO 입력(제한 패턴)에 어떻게 의존하는지 분석한다. 저 k1 체계에서 로직 응용을 위한 실용적 SMO 지침을 제공한다. (GLOBALFOUNDRIES)

## 주요 기여
- 소스 포인트 영향 인자(SPIF) 개념 도입으로 소스 픽셀별 기여도 분석
- 현실적 비용함수와 정확한 공정 데이터의 SMO 중요성 강조
- 리지스트 블러가 최적화 해에 미치는 영향 분석
- 로직 응용을 위한 SMO 실용 지침 및 한계 패턴 선택 방법론 제시

## 알고리즘/수식
**소스 포인트 영향 인자 (SPIF):**
$$SPIF_k = \left|\frac{\partial F}{\partial \sigma_k}\right|$$
비용함수 $F$에 대한 소스 픽셀 $\sigma_k$의 편미분 크기 — 소스 픽셀의 최적화 기여도.

**로직 응용 SMO 비용함수:**
$$F = \sum_{p \in \mathcal{P}_{logic}} w_p \cdot EPE_p^2(\boldsymbol{\sigma}, m_p)$$
랜덤 로직 패턴 집합 $\mathcal{P}_{logic}$에서 가중 EPE 합.

**리지스트 블러 포함 이미징 모델:**
$$I_{resist}(x) = I_{aerial}(x) * g_{resist}(x)$$
리지스트 블러 커널 $g_{resist}$로 에어리얼 이미지 컨볼루션.

**소스 최적화 (전역 소스):**
$$\min_{\boldsymbol{\sigma}} F(\boldsymbol{\sigma}) = \sum_p EPE_p^2(\boldsymbol{\sigma}, m_p^{fixed})$$
마스크 고정 상태에서 전역 소스 최적화.

**제한 패턴 (Limiting Pattern) 선택:**
높은 SPIF 값을 가지는 패턴 = 소스 최적화에 큰 영향을 미치는 제한 패턴:
$$\mathcal{P}_{limiting} = \{p : SPIF_p > SPIF_{threshold}\}$$

**k1 인자와 SMO 필요성:**
$$k_1 = \frac{CD \cdot NA}{\lambda} < 0.35 \rightarrow \text{SMO 필요}$$

## OPC 툴 SMO 구현 관련성
- SKOPC 로직 레이어 SMO에서 한계 패턴 선택 및 SPIF 분석 방법 참고
- `skopc/smo/spif_analysis.py`에 소스 포인트 영향 인자 계산 구현
- 리지스트 블러 포함 이미징 모델은 `skopc/litho/resist_blur.py`에 구현
- 로직/SRAM 혼합 레이아웃 SMO 전략 설계 시 Nagahara et al. 2010과 함께 참고

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Nagahara et al., "SMO 28nm logic," SPIE 2010
- Dam et al., "SMO theory to practice," SPIE 2010

## 태그
`SMO`, `SPIE`, `logic-applications`, `SPIF`, `source-point-impact-factor`, `random-logic`, `limiting-pattern`, `resist-blur`, `low-k1`, `GLOBALFOUNDRIES`, `process-window`
