# A Novel Contrast-Aware SMO at 7nm Technology Node

## 메타데이터
- **저자**: Xiaojing Su, Lisong Dong, Yayi Wei, Yajuan Su
- **연도**: 2022
- **게재지/학회**: Proc. SPIE 12052, DTCO and Computational Patterning, 120520H
- **DOI/URL**: https://doi.org/10.1117/12.2614140
- **인용수**: 확인 필요

## 핵심 요약
7nm 기술 노드에서 기존 EPE 기반 SMO 흐름에 이미지 로그 기울기(ILS, Image Log Slope) 및 ILS-DOF 페널티를 추가한 대비 인식 SMO(contrast-aware SMO)를 제안한다. EPE 기반 SMO는 공정 변동에 대한 강인성이 부족한 반면, ILS를 비용함수에 명시적으로 통합하여 노광 위도와 초점 심도를 동시에 향상시킨다.

## 주요 기여
- EPE 기반 SMO에 ILS/ILS-DOF 페널티 통합한 대비 인식 SMO
- 7nm 노드에서 이미지 대비(ILS) 향상으로 공정 강인성 개선
- ILS-DOF 페널티로 노광 위도 및 초점 심도 동시 최적화
- 기존 EPE-only SMO 대비 개선된 공정 윈도우 달성

## 알고리즘/수식
**대비 인식 SMO 비용함수:**
$$F_{CA-SMO}(\boldsymbol{\sigma}, m) = F_{EPE}(\boldsymbol{\sigma}, m) + \lambda_{ILS} F_{ILS}(\boldsymbol{\sigma}, m) + \lambda_{DOF} F_{ILS-DOF}(\boldsymbol{\sigma}, m)$$
EPE 항 + ILS 페널티 + ILS-DOF 페널티.

**이미지 로그 기울기 (ILS):**
$$ILS(x_j) = \frac{1}{I(x_j)} \left|\frac{\partial I}{\partial x}\right|_{x=x_j}$$
에지 포인트 $x_j$에서의 정규화 이미지 기울기.

**ILS 페널티:**
$$F_{ILS}(\boldsymbol{\sigma}, m) = \sum_j \max(0, ILS_{min} - ILS(x_j;\boldsymbol{\sigma},m))^2$$
최소 ILS 임계값 $ILS_{min}$ 이하 포인트 페널티.

**ILS-DOF 페널티 (초점 변동 포함):**
$$F_{ILS-DOF}(\boldsymbol{\sigma}, m) = \sum_j \sum_{\delta f \in \Delta F} w_f \max(0, ILS_{min} - ILS(x_j;\boldsymbol{\sigma},m;\delta f))^2$$

**ILS 그래디언트:**
$$\frac{\partial ILS_j}{\partial \sigma_k} = \frac{\partial}{\partial \sigma_k}\left[\frac{|\partial I_j/\partial x|}{I_j}\right]$$

**NILS (Normalized ILS):**
$$NILS_j = ILS_j \cdot CD_j$$
CD로 정규화한 이미지 로그 기울기.

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 이미지 대비 페널티 추가 시 대비 인식 SMO 참고
- `skopc/smo/contrast_aware_smo.py`에 ILS/NILS 페널티 포함 SMO 구현
- Xu et al. 2023 글로벌 NILS 제어 SMO, Zhang et al. 2024 LES NILS 페널티와 함께 NILS/ILS 기반 SMO 계열 참고

## 참고문헌 (핵심)
- Xu et al., \"Global NILS control SMO process window,\" Applied Optics 2023
- Zhang et al., \"SMO line-end shortening NILS,\" Applied Optics 2024
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011

## 태그
`SMO`, `SPIE`, `contrast-aware`, `ILS`, `NILS`, `image-log-slope`, `7nm`, `process-window`, `DOF`, `EL`, `EPE`, `ILS-DOF`
