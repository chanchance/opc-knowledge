# Global Optimization of the Illumination Distribution to Maximize Integrated Process Window

## 메타데이터
- **저자**: Alan E. Rosenbluth, Nakgeuon Seong
- **연도**: 2006
- **게재지/학회**: Proc. SPIE 6154, Optical Microlithography XIX, 61540H (15 March 2006)
- **DOI/URL**: https://doi.org/10.1117/12.656950
- **인용수**: 다수 (소스 최적화 분야 핵심 논문)

## 핵심 요약
리소그래피 공정 마진(process window)을 극대화하기 위한 조명 분포(illumination distribution)의 전역 최적화 방법을 제안한다. 포커스를 통한 공정 마진 관련 지표에 대해 전역 최적화를 확장하며, 특히 모든 패턴에 걸친 공통 ED(Exposure-Defocus) 윈도우 면적을 최대화하는 특정 소스 형상을 결정할 수 있다. 여러 패턴을 동시에 고려하는 통합 공정 마진(integrated process window) 개념을 도입한다.

## 주요 기여
- 포커스 공정 마진을 포함한 전역 소스 최적화로 기존 방법 확장
- 통합 공정 마진(integrated process window): 다중 패턴에 걸친 공통 ED 윈도우 최대화
- 전역 수렴 보장 알고리즘으로 소스 형상 최적화 (로컬 미니마 회피)
- 픽셀화 소스와 파라메트릭 소스 양쪽 최적화 지원

## 알고리즘/수식
**통합 공정 마진 목적함수:**
$$\max_{\sigma \geq 0} \quad IPW(\sigma) = \text{Area}\left\{(E,f) : \forall j, \, |CD_j(E,f;\sigma) - CD_{j,target}| \leq \Delta CD_{spec}\right\}$$
여기서 공통 ED 윈도우는 모든 패턴 $j$에 대해 동시에 스펙을 만족하는 영역.

**E-D 윈도우 기반 목적함수 (완화 형식):**
$$F(\sigma) = \sum_{E,f} \prod_j \mathbf{1}\left[|CD_j(E,f;\sigma) - CD_{j,target}| \leq \Delta CD_{spec}\right]$$

**소스-TCC 관계:**
$$TCC(\mathbf{f}_1; \mathbf{f}_2) = \sum_k \sigma_k H(\mathbf{f}_1 + \mathbf{f}_k) H^*(\mathbf{f}_2 + \mathbf{f}_k)$$
소스 픽셀 강도 $\sigma_k$ 변화 → TCC 선형 변화 → aerial image에 선형 영향.

**소스 최적화 (볼록 완화):**
소스 $\sigma$에 대한 TCC의 선형성을 활용:
$$F(\sigma) = \mathbf{c}^T \sigma + \text{const} \quad \Rightarrow \quad \sigma^* = \arg\min_{\sigma \geq 0, \sum \sigma_k = 1} \mathbf{c}^T \sigma$$
→ 선형 프로그래밍(LP)으로 전역 최적해 보장.

**포커스 공정 마진 통합:**
$$\max_{\sigma} \min_j \int_{-DOF/2}^{DOF/2} EL_j(f; \sigma) \, df$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO의 다중 패턴 통합 공정 마진 최적화 구현의 핵심 참고
- 소스-TCC 선형 관계를 이용한 볼록 최적화(LP/QP)로 전역 최적해 탐색
- `skopc/smo/integrated_pw.py` 구현 시 통합 공정 마진 계산 방법 직접 참조
- 포커스 범위 통합 목적함수 설계에 활용

## 참고문헌 (핵심)
- Rosenbluth et al., "Optimum mask and source patterns to print a given shape," JM3 2002
- Granik, "Source optimization for image fidelity and throughput," JM3 2004
- Socha et al., "Simultaneous source mask optimization," Proc. SPIE 5853, 2005

## 태그
`SMO`, `SPIE`, `IBM-Research`, `Rosenbluth`, `global-optimization`, `integrated-process-window`, `illumination-optimization`, `E-D-window`, `linear-programming`, `multi-pattern`, `TCC-linearity`
