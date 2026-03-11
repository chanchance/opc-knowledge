# An Innovative Source-Mask co-Optimization (SMO) Method for Extending Low k1 Imaging

## 메타데이터
- **저자**: Stephen Hsu, Luoqi Chen, Zhipan Li, Sean Park, Keith Gronlund, Hua-Yu Liu, Neal Callan, Robert Socha, Steve Hansen
- **연도**: 2008
- **게재지/학회**: Proc. SPIE 7140, Lithography Asia 2008, 714010 (4 December 2008)
- **DOI/URL**: https://doi.org/10.1117/12.806657
- **인용수**: 다수 (SMO 분야 초기 핵심 논문)

## 핵심 요약
저 k1 이미징 한계를 극복하기 위한 혁신적인 소스-마스크 동시 최적화(SMO) 방법을 제안한다. 기존의 순차적(iterative) 소스→마스크 최적화 방식과 새로운 동시(simultaneous) SMO 방식을 비교한다. 픽셀화 자유형 소스(freeform source)와 연속 전송 회색조 마스크(continuous transmission graytone mask)를 EPE 기반 비용함수로 동시 최적화하며, ASML FlexRay 조명기의 제약 조건을 적용한다.

## 주요 기여
- 순차적 SMO vs. 동시적 SMO 방법론 비교 및 동시 최적화의 우월성 실증
- 픽셀화 자유형 소스와 연속 회색조 마스크를 EPE 비용함수로 동시 최적화
- ASML 스캐너(NXE 계열) 특화 FlexRay 조명기 제약 조건 통합
- 공정 마진(process window) 유의미한 향상: 기존 iterative 방법 대비 개선

## 알고리즘/수식
**순차적 SMO 흐름:**
1. NILS(Normalized Image Log-Slope) 기반 소스 최적화
2. 최적화된 소스 하에 어시스트 피처(AF) 배치
3. OPC 수행
4. OPC된 레이아웃으로 소스 재최적화

**동시적 SMO 목적함수 (EPE 기반):**
$$F_{SMO} = \sum_{j \in \text{edge points}} EPE_j^2 + \lambda_s \|\sigma\|_1 + \lambda_m \|m - m_0\|^2$$

**자유형 소스 표현:**
$$\sigma = [\sigma_1, \sigma_2, ..., \sigma_N]^T, \quad 0 \leq \sigma_i \leq 1$$
ASML FlexRay DOE 제약: 소스 픽셀 강도는 DOE 제조 가능성 기준 충족 필요

**연속 회색조 마스크 투과율:**
$$m(x) \in [0, 1] \quad \text{(gray-tone, 이후 이진화)}$$

## OPC 툴 SMO 구현 관련성
- SKOPC SMO 모듈 설계 시 iterative vs. simultaneous 방식 선택의 근거 자료
- EPE 기반 비용함수 구현의 직접적 참고 (`skopc/smo/cost_functions.py`)
- 자유형 픽셀 소스 최적화의 시초 논문으로 소스 파라미터화 방법 참고
- ASML 스캐너 조명기 제약 조건 모델링 방법 제시

## 참고문헌 (핵심)
- Rosenbluth et al., "Optimum mask and source patterns to print a given shape," JM3 2002
- Hansen & Socha, "Source-mask optimization for low k1 lithography," Proc. SPIE 2004
-Granik, "Source optimization for image fidelity and throughput," JM3 2004

## 태그
`SMO`, `SPIE`, `source-mask-co-optimization`, `low-k1`, `freeform-illumination`, `EPE`, `FlexRay`, `ASML`, `pixelated-source`, `ArF-immersion`
