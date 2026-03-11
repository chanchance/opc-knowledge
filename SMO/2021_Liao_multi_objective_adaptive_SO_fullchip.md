# Multi-Objective Adaptive Source Optimization for Full Chip

## 메타데이터
- **저자**: Guanghui Liao, Yiyu Sun, Pengzhi Wei, Miao Yuan, Zhaoxuan Li, Yanqiu Li
- **연도**: 2021
- **게재지/학회**: Applied Optics, Vol. 60, No. 9, pp. 2530–2536
- **DOI/URL**: https://doi.org/10.1364/AO.418139
- **인용수**: 다수

## 핵심 요약
전체 칩(full chip) 규모에서 압축 센싱과 등고선 샘플링을 결합하여 픽셀 조명 소스 패턴을 빠르게 최적화하면서 각 클립의 이미징 충실도를 동시에 보장하는 다목적 적응형 소스 최적화(adaptive-MOSO) 방법을 최초로 제안한다. 클립별 적응형 가중치 분배로 대규모 칩의 리소그래피 성능을 향상시킨다.

## 주요 기여
- 전체 칩 규모 다목적 적응형 소스 최적화(adaptive-MOSO) 최초 제안
- 등고선 샘플링 + 압축 센싱으로 전체 칩 소스 최적화 가속
- 클립별 적응형 가중치로 각 레이아웃 패턴의 이미징 충실도 보장
- 대규모 칩 리소그래피 성능 향상 실증

## 알고리즘/수식
**다목적 SO 비용함수 (전체 칩):**
$$\min_{\boldsymbol{\sigma}} F_{total} = \sum_{c=1}^{N_{clips}} w_c F_c(\boldsymbol{\sigma})$$
$N_{clips}$개 클립의 가중 비용함수 합. $w_c$는 클립 $c$의 적응형 가중치.

**클립별 비용함수:**
$$F_c(\boldsymbol{\sigma}) = \sum_{j \in \Omega_c} \left(I(x_j; \boldsymbol{\sigma}, m_c) - I_{target,c}(x_j)\right)^2$$

**적응형 가중치 업데이트:**
$$w_c^{(t+1)} = w_c^{(t)} \cdot \left(1 + \alpha \cdot \frac{F_c^{(t)}}{F_{avg}^{(t)}}\right)$$
현재 클립 비용이 평균보다 높으면 가중치 증가 → 어려운 패턴에 집중.

**등고선 샘플링 (CS) 기반 빠른 SO:**
$$\boldsymbol{\sigma}^* = \arg\min_{\boldsymbol{a}} \|\boldsymbol{a}\|_1 \quad \text{s.t.} \quad \sum_c \|T_{c,CCS} \Phi \boldsymbol{a} - \boldsymbol{b}_{c,CCS}\|^2 \leq \epsilon_{total}$$
전체 클립의 등고선 샘플링 측정값을 동시에 만족하는 스파스 소스 탐색.

**소스 그래디언트 (다목적):**
$$\frac{\partial F_{total}}{\partial \sigma_k} = \sum_c w_c \frac{\partial F_c}{\partial \sigma_k}$$

## OPC 툴 SMO 구현 관련성
- SKOPC 전체 칩 SMO에서 클립별 적응형 가중치 다목적 소스 최적화 구현 참고
- `skopc/smo/multi_obj_adaptive_so.py`에 클립 라이브러리 기반 다목적 SO 구현
- 클립별 가중치 적응은 어려운 패턴(핫스팟)에 자동 집중하는 전략으로 활용
- Tsai et al. 2011 전체 칩 SMO 플로우와 결합하여 클립 기반 다목적 SO 설계 참고

## 참고문헌 (핵심)
- Song et al., "Inverse litho source opt CS," Optics Express 2014
- Sun et al., "CCS-BCS fast SO," Optics Express 2019
- Tsai et al., "Full-chip SMO ASML Brion," SPIE 2011

## 태그
`SMO`, `Applied-Optics`, `multi-objective`, `adaptive-weight`, `full-chip`, `compressive-sensing`, `contour-sampling`, `source-optimization`, `clip-library`, `hotspot`, `computational-efficiency`
