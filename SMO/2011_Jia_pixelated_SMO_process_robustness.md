# Pixelated Source Mask Optimization for Process Robustness in Optical Lithography

## 메타데이터
- **저자**: Ningning Jia, Edmund Y. Lam
- **연도**: 2011
- **게재지/학회**: Optics Express, Vol. 19, No. 20, pp. 19384–19398 (2011) [PubMed PMID: 21996879]
- **DOI/URL**: https://doi.org/10.1364/OE.19.019384
- **인용수**: 다수

## 핵심 요약
공정 변동(process variation)에 강건한 자유형 소스 및 마스크 패턴을 역 이미징(inverse imaging) 방법으로 설계하는 픽셀 기반 SMO 방법을 제안한다. 패턴 충실도와 aerial image 강도 분포를 통합하는 비용함수를 개발하고, 소스와 마스크의 교번 최적화를 통계적 SMO 프레임워크로 해결한다. 포커스, 도즈 변동에 대한 강건성을 명시적으로 목적함수에 포함한다.

## 주요 기여
- 공정 변동(포커스/도즈)에 대한 강건성을 비용함수에 명시적 통합
- 패턴 충실도 + aerial image 강도 분포를 결합한 통합 비용함수 설계
- 통계적 SMO 프레임워크: 공정 조건 샘플링 기반 강건 최적화
- 픽셀 기반 자유형 소스와 마스크 교번 최적화로 강건한 SMO 달성

## 알고리즘/수식
**통계적 강건 SMO 비용함수:**
$$F_{robust} = \mathbb{E}_{(d,f) \sim \mathcal{P}} \left[\sum_j EPE_j^2(d, f; \sigma, m)\right]$$
여기서 $(d, f)$는 도즈/포커스 확률 분포 $\mathcal{P}$에서 샘플링.

**이산화 근사:**
$$F_{robust} \approx \sum_{i=1}^{N_{sample}} w_i \sum_j EPE_j^2(d_i, f_i; \sigma, m)$$
$(d_i, f_i)$는 공정 조건 샘플 포인트, $w_i$는 가중치.

**통합 비용함수 (패턴 충실도 + 강도 분포):**
$$F = F_{EPE}(\sigma, m) + \lambda_{ILS} F_{ILS}(\sigma, m) + \lambda_{robust} F_{robust}(\sigma, m)$$

**교번 최적화:**
1. 마스크 $m$ 고정 → 소스 $\sigma$ 그래디언트 최적화
2. 소스 $\sigma$ 고정 → 마스크 $m$ 그래디언트 최적화
3. 강건성 평가 및 수렴 판정

**도즈-포커스 샘플링:**
$$\{(d_i, f_i)\} = \text{Gauss}(\mu_d, \sigma_d) \times \text{Gauss}(\mu_f, \sigma_f)$$

## OPC 툴 SMO 구현 관련성
- SKOPC RSMO 구현 시 공정 변동 강건성을 비용함수에 통합하는 방법 참고
- `skopc/smo/robust_smo.py`에서 통계적 샘플링 기반 강건 최적화 구현
- 도즈/포커스 변동 조건 샘플링 방법을 `skopc/smo/process_variation.py`에 구현 가능
- Hashimoto(2013) RSMO와 함께 강건 SMO 구현의 핵심 참고 논문

## 참고문헌 (핵심)
- Peng et al., "Gradient-based SMO," IEEE TIP 2011
- Hsu et al., "An innovative SMO method," Proc. SPIE 7140, 2008
- Li & Lam, "Efficient SMO with augmented Lagrangian," Optics Express 2013

## 태그
`SMO`, `robust-SMO`, `process-robustness`, `statistical-SMO`, `dose-focus-variation`, `pixelated-source`, `inverse-imaging`, `Optics-Express`, `process-window`, `alternating-optimization`
