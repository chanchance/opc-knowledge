# High-Fidelity Source Mask Optimization for Suppressing Line-End Shortening

## 메타데이터
- **저자**: Zhiwei Zhang, Miao Yuan, Zhaoxuan Li, Weichen Huang, He Yang, Zhen Li, Yanqiu Li
- **연도**: 2024
- **게재지/학회**: Applied Optics, Vol. 63, No. 2, pp. 327–337
- **DOI/URL**: https://doi.org/10.1364/AO.506473
- **인용수**: 확인 필요

## 핵심 요약
라인 끝 단축(line-end shortening, LES) 억제를 위해 라인 끝 영역에 적응형 가중치를 적용하고 NILS 기반 패널티 항을 포함한 비용함수를 설계하는 고충실도 SMO 방법을 제안한다. 매 반복에서 EPE에 따라 라인 끝 가중치를 적응적으로 업데이트하는 하이브리드 가중치 방법으로, 전체 피처 충실도를 유지하면서 라인 끝 영역에 집중적으로 최적화한다.

## 주요 기여
- 라인 끝 EPE에 따른 적응형 하이브리드 가중치 방법으로 LES 억제
- NILS 기반 패널티 항 포함 비용함수로 전체 피처 충실도 보장
- 매 반복마다 가중치 적응적 업데이트로 LES 억제와 전체 충실도 균형 달성
- 기존 SMO 대비 LES 효과적 억제 및 리소그래피 충실도 향상 실증

## 알고리즘/수식
**적응형 하이브리드 가중치 SMO 비용함수:**
$$F = \sum_{j \notin \Omega_{LE}} EPE_j^2 + \sum_{j \in \Omega_{LE}} w_j^{(t)} EPE_j^2 + \lambda_{NILS} F_{NILS}$$
라인 끝 영역 $\Omega_{LE}$의 가중치 $w_j^{(t)}$를 적응적으로 업데이트.

**적응형 라인 끝 가중치 업데이트:**
$$w_j^{(t+1)} = w_j^{(t)} + \Delta w \cdot \mathbb{1}\left[EPE_j^{(t)} > EPE_{th}\right]$$
현재 EPE가 임계값 $EPE_{th}$를 초과하는 라인 끝 포인트의 가중치 증가.

**NILS 패널티 항:**
$$F_{NILS} = \sum_j \max\left(0, NILS_{min} - NILS_j\right)^2$$
$$NILS_j = \frac{CD_j}{I(x_j)} \left|\frac{\partial I}{\partial x}\right|_{x_j}$$
최소 NILS 값 이하 포인트에 패널티 부과.

**라인 끝 단축 정의:**
$$LES = L_{nominal} - L_{printed}$$
설계 라인 길이 $L_{nominal}$ 대비 실제 인쇄된 길이 $L_{printed}$의 차이.

**소스/마스크 그래디언트 (가중 EPE):**
$$\frac{\partial F}{\partial \sigma_k} = \sum_j 2 w_j EPE_j \frac{\partial EPE_j}{\partial \sigma_k} + \lambda_{NILS} \frac{\partial F_{NILS}}{\partial \sigma_k}$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO에서 라인 끝 단축 억제 적응형 가중치 전략 구현 시 참고
- `skopc/smo/les_aware_smo.py`에 라인 끝 검출 및 적응형 가중치 SMO 구현
- NILS 패널티 항은 `skopc/smo/nils_penalty.py`로 모듈화하여 다른 SMO에도 적용 가능
- 라인 끝 단축은 로직 레이어 OPC에서 중요한 패턴 오차 유형으로 실용적 관련성 높음

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Ma et al., "Pixelated SMO immersion," JOSAA 2013
- Shen et al., "Adaptive gradient SMO process awareness," Chinese Optics Letters 2019

## 태그
`SMO`, `Applied-Optics`, `line-end-shortening`, `LES`, `adaptive-weight`, `NILS`, `penalty-term`, `high-fidelity`, `EPE`, `pattern-fidelity`, `logic-layer`
