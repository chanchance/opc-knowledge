# Full-Chip Source and Mask Optimization

## 메타데이터
- **저자**: Min-Chun Tsai, Stephen Hsu, Luoqi Chen, Yen-Wen Lu, Jiangwei Li, Frank Chen, Hong Chen, Jun Tao, Been-Der Chen, Hanying Feng, William Wong, Wei Yuan, Xiaoyang Li, Zhipan Li, Liang Li, Russell Dover, Hua-yu Liu, Jim Koonmen
- **연도**: 2011
- **게재지/학회**: Proc. SPIE 7973, Optical Microlithography XXIV, 79730A
- **DOI/URL**: https://doi.org/10.1117/12.881633
- **인용수**: 다수

## 핵심 요약
전체 칩 규모에서 소스 최적화와 유연 마스크 최적화(FMO, Flexible Mask Optimization)를 결합한 비용 효율적인 풀칩 SMO 방법을 제안한다. 임계 클립 선택으로 대표 패턴을 식별한 후 SMO로 소스를 최적화하고, FMO 프레임워크는 공정 변동 민감도에 따라 칩 영역별로 다른 OPC 기법을 적용하여 최적 공정 성능과 테이프아웃/마스크 비용을 균형 있게 달성한다. ASML Brion Technologies.

## 주요 기여
- 풀칩 SMO + 유연 마스크 최적화(FMO) 통합 프레임워크 제안
- 임계 클립 선택 기법으로 대표 패턴 식별 및 효율적 소스 최적화
- FMO: 칩 영역 민감도에 따른 OPC 기법 차등 적용
- 최적 공정 성능과 마스크 비용의 균형 달성

## 알고리즘/수식
**임계 클립 선택 기반 풀칩 SMO:**
$$\boldsymbol{\sigma}^* = \arg\min_\sigma \sum_{c \in \mathcal{C}_{critical}} F_{EPE}(\boldsymbol{\sigma}, m_c)$$
임계 클립 집합 $\mathcal{C}_{critical}$에서 소스 최적화.

**풀칩 클립 분류:**
$$\mathcal{C}_{critical} = \{c : \text{yield-sensitivity}(c) > \theta_{critical}\}$$
수율 민감도 임계값 $\theta_{critical}$ 초과 패턴을 임계 클립으로 분류.

**유연 마스크 최적화 (FMO):**
$$m^*(x) = \begin{cases} m_{advanced-OPC}(x) & x \in \Omega_{sensitive} \\ m_{rule-OPC}(x) & x \in \Omega_{standard} \end{cases}$$
민감 영역 $\Omega_{sensitive}$에는 고급 OPC, 일반 영역엔 룰 기반 OPC 적용.

**영역 민감도 분류:**
$$\Omega_{sensitive} = \{x : \text{PV-band-width}(x; \boldsymbol{\sigma}^*) > \Delta_{PV,th}\}$$
PV(공정 변동) 밴드폭이 임계값 초과 영역을 민감 영역으로 분류.

**비용함수 (SMO 소스 최적화):**
$$F(\boldsymbol{\sigma}) = \sum_{c \in \mathcal{C}_{crit}} \sum_j EPE_j^2(\boldsymbol{\sigma}, m_c)$$

## OPC 툴 SMO 구현 관련성
- SKOPC 풀칩 SMO에서 임계 클립 선택 및 FMO 프레임워크 참고
- `skopc/smo/fullchip_smo_fmo.py`에 FMO 칩 영역 분류 및 차등 OPC 적용 구현
- 임계 클립 선택은 `skopc/smo/critical_clip_selection.py`에 구현
- Tsai et al. 2011 풀칩 SMO ASML Brion(기존 수집)과 함께 ASML Brion 풀칩 SMO 계열 참고

## 참고문헌 (핵심)
- Tsai et al., \"Fullchip SMO ASML Brion,\" SPIE 2011
- Peng et al., \"Gradient-based SMO,\" IEEE TIP 2011
- Liao et al., \"Critical pattern selection fullchip SMO,\" Optics Express 2020

## 태그
`SMO`, `SPIE`, `full-chip`, `FMO`, `flexible-mask-optimization`, `critical-clip-selection`, `ASML-Brion`, `process-window`, `PV-band`, `OPC`, `yield-optimization`
