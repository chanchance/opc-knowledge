# Full-Chip Source and Mask Optimization

## 메타데이터
- **저자**: Min-Chun Tsai, Stephen Hsu, Luoqi Chen (외, ASML Brion Technologies)
- **연도**: 2011
- **게재지/학회**: Proc. SPIE 7973, Optical Microlithography XXIV, 79730A (22 March 2011)
- **DOI/URL**: https://doi.org/10.1117/12.881633
- **인용수**: 다수

## 핵심 요약
전체 칩(full-chip) 스케일에서 비용 효율적인 소스-마스크 최적화를 위한 2단계 방법을 제안한다. 첫 번째 단계에서 픽셀화 자유형 소스와 연속 회색조 마스크를 EPE 비용함수로 동시 최적화하고, ASML 스캐너 제약 조건을 적용한다. 두 번째 단계에서 최적화된 회색조 마스크에서 어시스트 피처(AF) "씨앗(seeds)"을 추출하여 메인 피처와 함께 공정 마진 및 MEEF 요건을 만족하도록 최적화한다 (FMO: Flexible Mask Optimization).

## 주요 기여
- 전체 칩 SMO를 위한 두 단계 방법: ① 소스+그레이톤 마스크 동시 최적화 → ② FMO(Flexible Mask Optimization)
- 최적화된 그레이톤 마스크에서 SRAF "씨앗" 자동 추출 방법
- ASML 스캐너 FlexRay 조명기 제약 조건 통합
- 전체 칩 규모에서 실용적인 SMO 플로우 실증 (ASML Tachyon SMO 상업화 기반)

## 알고리즘/수식
**단계 1: 소스 + 그레이톤 마스크 동시 최적화:**
$$\min_{\sigma, m_{gray}} F_{EPE}(\sigma, m_{gray}) = \sum_j EPE_j^2(\sigma, m_{gray})$$
s.t. $0 \leq \sigma_k \leq 1$ (소스 강도), $m_{gray}(x) \in [0,1]$ (회색조 투과율)

**FlexRay 소스 제약:**
$$\sigma \in \mathcal{S}_{FlexRay}: \text{ASML 조명기 제조 가능 소스 집합}$$

**SRAF 씨앗 추출:**
최적화된 회색조 마스크 $m_{gray}$에서:
$$m_{binary}(x) = \begin{cases} 1 & m_{gray}(x) > \theta_{main} \\ 0.5 & \theta_{SRAF} < m_{gray}(x) \leq \theta_{main} \text{ (SRAF 후보)} \\ 0 & m_{gray}(x) \leq \theta_{SRAF} \end{cases}$$

**단계 2: FMO (SRAF + 메인 피처 최적화):**
$$\min_{AF, m_{main}} F_{PW}(AF, m_{main}) + \lambda_{MEEF} \sum_j MEEF_j^2$$
SRAF 위치/크기 $AF$와 메인 피처 $m_{main}$을 공정 마진 목적함수로 최적화.

**전체 칩 확장:**
클립 기반 SMO → 레이아웃 전체로 소스 적용 → 전체 칩 FMO.

## OPC 툴 SMO 구현 관련성
- SKOPC SMO의 전체 칩 플로우 설계 시 직접 참고 (산업 표준 플로우)
- 그레이톤 마스크에서 SRAF 씨앗 자동 추출 방법을 `skopc/smo/sraf_extraction.py`에 구현 가능
- 2단계 SMO 플로우(글로벌 소스+마스크 → 로컬 SRAF 정밀화)는 SKOPC SMO 아키텍처의 기준
- FMO 개념은 `skopc/smo/flexible_mask_opt.py` 구현 참고

## 참고문헌 (핵심)
- Hsu et al., "An innovative SMO method," Proc. SPIE 7140, 2008
- Nagahara et al., "SMO for 28nm logic," Proc. SPIE 7640, 2010
- Dam et al., "SMO from theory to practice," Proc. SPIE 7640, 2010

## 태그
`SMO`, `SPIE`, `full-chip-SMO`, `ASML-Brion`, `Tachyon-SMO`, `graytone-mask`, `SRAF-extraction`, `FMO`, `FlexRay`, `EPE`, `process-window`, `MEEF`, `two-stage-SMO`
