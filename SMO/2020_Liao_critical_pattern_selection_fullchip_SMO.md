# Critical Pattern Selection Method for Full-Chip Source and Mask Optimization

## 메타데이터
- **저자**: Lufeng Liao, Sikun Li, Xiangzhao Wang, Libin Zhang, Pengzheng Gao, Yayi Wei, Weijie Shi
- **연도**: 2020
- **게재지/학회**: Optics Express, Vol. 28, No. 14, pp. 20748–20763
- **DOI/URL**: https://doi.org/10.1364/OE.398848
- **인용수**: 다수

## 핵심 요약
전체 칩 SMO를 위한 회절 기반 임계 패턴 선택(Critical Pattern Selection) 방법을 제안한다. 회절 서명(diffraction-signature)을 8방향 폭으로 기술하고, 회절 서명 간 커버리지 규칙을 설계하며, 그룹화 방법과 패턴 선택 전략을 제안한다. SIOM/CAS의 전체 칩 SMO를 위한 실용적 클립 선택 자동화 방법이다.

## 주요 기여
- 회절 서명(diffraction-signature) 기반 새로운 임계 패턴 선택 방법 제안
- 8방향 폭으로 회절 서명 기술하여 패턴 특성화
- 회절 서명 커버리지 규칙으로 대표 패턴 자동 선택
- 전체 칩 SMO를 위한 실용적 클립 라이브러리 구축 자동화

## 알고리즘/수식
**회절 서명 정의:**
마스크 패턴 $m$의 회절 스펙트럼 $M(f,g) = \mathcal{F}[m](f,g)$에서:
$$DS(\theta_i) = \int_{\theta_i - \Delta\theta/2}^{\theta_i + \Delta\theta/2} |M(\rho, \theta)|^2 d\theta, \quad i = 1, \ldots, 8$$
8방향 $\theta_i = i\pi/4$에서의 회절 에너지 분포.

**회절 서명 벡터:**
$$\boldsymbol{DS} = [DS(\theta_1), DS(\theta_2), \ldots, DS(\theta_8)]^T$$
패턴의 대표 회절 특성 8차원 벡터.

**커버리지 규칙:**
패턴 $p_i$가 패턴 $p_j$를 커버(cover)하는 조건:
$$\forall k: DS_k(p_i) \geq DS_k(p_j) \cdot (1 - \epsilon_{cover})$$
$p_i$의 회절 서명이 $p_j$보다 각 방향에서 크거나 같을 때 $p_i$가 $p_j$를 커버.

**패턴 선택 전략:**
```
1. 전체 칩에서 모든 패턴의 회절 서명 DS 계산
2. DS 기반 클러스터링으로 유사 패턴 그룹화
3. 각 그룹에서 가장 어려운 패턴(worst case) 선택
4. 커버리지 규칙으로 중복 제거
5. 선택된 임계 패턴으로 SMO 클립 라이브러리 구성
```

**SMO 클립 라이브러리 기반 최적화:**
$$\min_{\boldsymbol{\sigma}, m} F = \sum_{c \in \mathcal{C}_{selected}} F_c(\boldsymbol{\sigma}, m_c)$$
선택된 임계 패턴 집합 $\mathcal{C}_{selected}$에 대해서만 SMO 수행.

## OPC 툴 SMO 구현 관련성
- SKOPC 전체 칩 SMO에서 임계 패턴 자동 선택 구현 시 핵심 참고
- `skopc/smo/critical_pattern_selection.py`에 회절 서명 기반 패턴 선택 구현
- 회절 서명 8방향 벡터는 `skopc/litho/diffraction_signature.py`로 모듈화
- 클립 라이브러리 자동 구축으로 전체 칩 SMO 실행 시간 대폭 절감 가능

## 참고문헌 (핵심)
- Tsai et al., "Full-chip SMO ASML Brion," SPIE 2011
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Liao et al., "Multi-objective adaptive SO full chip," Applied Optics 2021

## 태그
`SMO`, `Optics-Express`, `critical-pattern-selection`, `full-chip-SMO`, `diffraction-signature`, `clip-library`, `pattern-clustering`, `coverage-rule`, `SIOM`, `CAS`, `computational-efficiency`
