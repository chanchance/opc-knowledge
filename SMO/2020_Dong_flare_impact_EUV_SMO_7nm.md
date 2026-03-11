# Impact of Flare on Source Mask Optimization in EUVL for 7nm Technology Node

## 메타데이터
- **저자**: Lisong Dong, Rui Chen, Taian Fan, Rongbo Zhao, Yayi Wei, Jianjun Jia, Zac Levinson, Thuc Dam, Jay Lee, Yongdong Wang, Larry Melvin
- **연도**: 2020
- **게재지/학회**: Proc. SPIE 11323, Extreme Ultraviolet (EUV) Lithography XI, 113232E
- **DOI/URL**: https://doi.org/10.1117/12.2552008
- **인용수**: 확인 필요

## 핵심 요약
EUV 리소그래피에서 짧은 파장과 미러 표면 거칠기로 인해 발생하는 플레어(flare)가 7nm 노드 SMO에 미치는 영향을 분석한다. 노광 필드 전반의 다양한 플레어 수준을 수치 시뮬레이션으로 상세히 분석하고, 플레어를 SMO 비용함수에 통합하여 플레어 강인성을 갖춘 EUV SMO 방법론을 개발한다.

## 주요 기여
- EUV 플레어가 7nm SMO 결과에 미치는 영향 정량화
- 노광 필드 위치별 플레어 수준 수치 분석
- 플레어 강인 EUV SMO 비용함수 개발
- Synopsys SMO 툴을 이용한 플레어 포함 EUV SMO 시뮬레이션

## 알고리즘/수식
**EUV 플레어 이미징 모델:**
$$I_{flare}(x) = (1-f) \cdot I_{aerial}(x) + f \cdot \bar{I}_{background}$$
플레어 비율 $f$와 배경 강도 $\bar{I}_{background}$.

**공간 플레어 분포 모델:**
$$F(x) = \int I_{aerial}(x') \cdot PSF_{flare}(x-x') dx'$$
플레어 점 확산 함수 $PSF_{flare}$와의 컨볼루션.

**플레어 강인 SMO 비용함수:**
$$F_{flare-SMO}(\boldsymbol{\sigma}, m) = \sum_{f \in \mathcal{F}} w_f \sum_j EPE_j^2(\boldsymbol{\sigma}, m; f)$$
플레어 수준 집합 $\mathcal{F}$에 대한 가중 EPE 합.

**EUV 강도 (플레어 포함):**
$$I(x; f) = (1-f) \cdot I_{ideal}(x; \boldsymbol{\sigma}, m) + f \cdot \bar{I}$$

**플레어 민감도 분석:**
$$S_f = \frac{\partial EPE}{\partial f}\bigg|_{f=f_{nominal}}$$
플레어 수준에 대한 EPE 민감도.

## OPC 툴 SMO 구현 관련성
- SKOPC EUV SMO에서 플레어 강인성 구현 시 참고
- `skopc/litho/euv_flare_model.py`에 EUV 플레어 이미징 모델 구현
- `skopc/smo/flare_robust_smo.py`에 플레어 강인 SMO 비용함수 구현
- Han et al. 2015 소스 블러+플레어 강인 HSMO와 함께 플레어 강인 SMO 계열 참고

## 참고문헌 (핵심)
- Han et al., \"Robust HSMO source blur flare,\" Applied Optics 2015
- Liu et al., \"EUV SMO 7nm node,\" SPIE 2014
- Ma et al., \"Gradient SMO EUV,\" IEEE TCI 2019

## 태그
`SMO`, `EUV`, `SPIE`, `flare`, `flare-robust`, `7nm`, `EUV-flare`, `process-window`, `Synopsys`, `mirror-roughness`, `background-intensity`
