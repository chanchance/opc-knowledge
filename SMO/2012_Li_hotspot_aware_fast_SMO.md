# Hotspot-Aware Fast Source and Mask Optimization

## 메타데이터
- **저자**: Jia Li, Yijiang Shen, Edmund Y. Lam
- **연도**: 2012
- **게재지/학회**: Optics Express, Vol. 20, No. 19, pp. 21792–21804
- **DOI/URL**: https://doi.org/10.1364/OE.20.021792
- **인용수**: 다수

## 핵심 요약
마스크 패턴 전체에서 동일한 영역에 대한 불필요한 최적화로 인한 긴 실행 시간을 해결하기 위해 핫스팟(hotspot) 인식 가중 SMO 방법을 제안한다. 핫스팟을 식별하고 비용함수에 가중 행렬을 결합하여 핫스팟 영역에 집중적으로 최적화하면서 공정 변동에 대한 강인성을 동시에 달성한다. 홍콩대 OPTIMA 그룹의 SMO 연구.

## 주요 기여
- 핫스팟 인식 가중 SMO 방법으로 최적화 효율 향상
- 핫스팟 영역 식별 및 가중 행렬 기반 비용함수 설계
- 공정 변동 강인성과 핫스팟 집중 최적화 동시 달성
- 전체 마스크 패턴 대비 실행 시간 단축

## 알고리즘/수식
**핫스팟 인식 SMO 비용함수:**
$$F_{HS} = \sum_j W_j \cdot EPE_j^2(\boldsymbol{\sigma}, m)$$
가중 행렬 $W_j$로 핫스팟 영역에 높은 가중치 부여.

**핫스팟 가중치 행렬:**
$$W_j = \begin{cases} w_{hot} & x_j \in \Omega_{hotspot} \\ w_{normal} & x_j \notin \Omega_{hotspot} \end{cases}, \quad w_{hot} \gg w_{normal}$$
핫스팟 포인트 집합 $\Omega_{hotspot}$에 높은 가중치 $w_{hot}$ 부여.

**핫스팟 식별:**
공칭 리소그래피 조건에서 EPE 임계값 초과 포인트를 핫스팟으로 식별:
$$\Omega_{hotspot} = \{x_j : |EPE_j^{nominal}| > EPE_{th}\}$$

**공정 변동 강인성 포함:**
$$F_{total} = F_{HS} + \lambda_{robust} F_{variation}$$
핫스팟 비용함수에 공정 변동 강인성 항 추가.

**그래디언트 기반 최적화:**
$$\frac{\partial F_{HS}}{\partial \sigma_k} = \sum_j W_j \cdot 2 EPE_j \cdot \frac{\partial EPE_j}{\partial \sigma_k}$$

**빠른 SMO 전략:**
핫스팟 포인트만 EPE 평가 → 계산량 감소:
$$|\Omega_{hotspot}| \ll |\Omega_{all}|$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 핫스팟 인식 가중 비용함수 설계 시 핵심 참고
- `skopc/smo/hotspot_aware_smo.py`에 핫스팟 식별 및 가중 SMO 구현
- 핫스팟 영역 집중 최적화는 전체 칩 SMO 실행 시간 단축에 효과적
- Li & Lam 2013 증강 라그랑지안 SMO와 함께 HKU Optima 그룹 SMO 계열 참고

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Li & Lam, "Efficient SMO augmented Lagrangian," Optics Express 2013
- Jia & Lam, "Pixelated SMO process robustness," Optics Express 2011

## 태그
`SMO`, `Optics-Express`, `hotspot-aware`, `weighted-SMO`, `fast-SMO`, `hotspot`, `process-robustness`, `gradient-based`, `HKU`, `Optima`, `weighted-cost-function`
