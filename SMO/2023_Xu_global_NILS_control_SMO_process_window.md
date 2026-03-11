# Initiative Global NILS Control in Source and Mask Optimization for Process Window Enhancement

## 메타데이터
- **저자**: Yiduo Xu, Fei Peng, Yi Song, Yan Zhao
- **연도**: 2023
- **게재지/학회**: Applied Optics, Vol. 62, pp. 2227–2236
- **DOI/URL**: https://doi.org/10.1364/AO.482501
- **인용수**: 확인 필요

## 핵심 요약
역 리소그래피(inverse lithography)에 NILS(Normalized Image Log Slope)를 패널티 함수로 통합하여 NILS의 지속적 증가를 보장함으로써 노광 위도(exposure latitude)를 확대하고 공정 마진을 향상시키는 SMO 방법을 제안한다. 두 가지 마스크 레이아웃에서 NILS가 각각 16%와 9% 향상되고, 노광 위도가 각각 21.5%와 21.7% 향상됨을 실증한다.

## 주요 기여
- NILS를 역 리소그래피 비용함수에 주도적(initiative) 제어 항으로 통합
- NILS 패널티 함수로 최적화 전 과정에서 NILS 단조 증가 보장
- 패턴 충실도 유지하면서 노광 위도 21% 이상 향상 실증
- 두 가지 대표 마스크 레이아웃에서 일관된 성능 향상 검증

## 알고리즘/수식
**NILS 포함 SMO 비용함수:**
$$F = F_{EPE}(\boldsymbol{\sigma}, m) + \lambda_{NILS} F_{NILS}(\boldsymbol{\sigma}, m)$$

**NILS 정의:**
$$NILS(x_j) = CD_j \cdot ILS(x_j) = CD_j \cdot \frac{1}{I(x_j)} \left|\frac{\partial I}{\partial x}\right|_{x_j}$$
이미지 로그 기울기(ILS)에 임계 치수 $CD_j$ 곱.

**NILS 패널티 항:**
$$F_{NILS} = \sum_j \max\left(0, NILS_{target} - NILS_j(\boldsymbol{\sigma}, m)\right)^2$$
목표 NILS 이하의 포인트에 패널티 부과 → 전역 NILS 증가 유도.

**NILS 그래디언트 (소스):**
$$\frac{\partial F_{NILS}}{\partial \sigma_k} = -2\sum_j \mathbb{1}[NILS_j < NILS_{target}] \cdot (NILS_{target} - NILS_j) \cdot \frac{\partial NILS_j}{\partial \sigma_k}$$

**NILS와 노광 위도 관계:**
$$EL \approx \frac{2 \cdot NILS \cdot \Delta CD_{allowed}}{CD}$$
NILS 증가 → 노광 위도 비례 증가.

**성능 결과:**
- NILS 향상: 패턴 1에서 16%, 패턴 2에서 9%
- 노광 위도(EL) 향상: 패턴 1에서 21.5%, 패턴 2에서 21.7%

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 NILS 기반 공정 마진 향상 비용함수 구현 시 참고
- `skopc/smo/nils_smo.py`에 전역 NILS 제어 SMO 구현
- NILS 패널티는 Zhang et al. 2024 라인 끝 SMO와 결합하여 복합 충실도 최적화 가능
- 노광 위도 향상이 목표인 SMO에서 NILS를 직접 제어 변수로 활용하는 전략 제공

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Jia & Lam, "Pixelated SMO process robustness," Optics Express 2011
- Zhang et al., "High-fidelity SMO LES," Applied Optics 2024

## 태그
`SMO`, `Applied-Optics`, `NILS`, `normalized-image-log-slope`, `process-window`, `exposure-latitude`, `penalty-function`, `gradient-based`, `pattern-fidelity`, `ILS`, `inverse-lithography`
