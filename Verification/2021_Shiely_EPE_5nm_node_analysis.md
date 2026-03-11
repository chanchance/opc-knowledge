# Analysis of Edge Placement Error (EPE) at the 5nm Node and Beyond

## 메타데이터
- **저자**: James Shiely et al.
- **연도**: 2021
- **게재지**: IEEE IITC/MAM (International Interconnect Technology Conference / Materials for Advanced Metallization), IEEE Xplore 9537543
- **DOI/URL**: https://ieeexplore.ieee.org/document/9537543/
- **인용수**: 다수 (5nm 노드 EPE 분석 기준 논문)

## 핵심 요약
5nm 노드 SRAM의 Via 0(V0) 레이어와 Metal 0(M0) 레이어 정렬에 대한 EPE를 상세히 분석한다. 두 레이어는 SMO(Source Mask Optimization)로 최적화되며, EPE는 스토캐스틱, 전역 CDU, 오버레이, OPC 오차, 스캐너 매칭 오차 등 모든 기여 요인을 포함하여 최소화된다. EPE의 최대 기여 요인은 스토캐스틱 EPE(SEPE)로 최대 5nm로 분석되며, SEPE 저감이 어려운 만큼 오버레이 EPE 저감에 더 집중해야 함을 제시한다.

## 주요 기여
1. 5nm 노드에서 EPE 구성 요소 별 정량적 기여도 분해 분석
2. 스토캐스틱 EPE(SEPE)가 최대 기여 요인(최대 5nm)임을 실증
3. SMO와 EPE 예산(Budget) 배분의 연계 방법론 제시
4. 5nm 이후 노드의 EPE 제어 과제 및 기술 방향 도출

## 검증 방법론
- **EPE 예산 분해(Budget Breakdown)**:
  - `EPE_total = SEPE + EPE_gCDU + EPE_overlay + EPE_OPC + EPE_scanner_matching`
  - 각 기여 요인을 통계적으로 정량화 (RSS 합산 또는 선형 합산)
- **스토캐스틱 EPE(SEPE)**: EUV 광자 샷 노이즈와 레지스트 흡수 통계에 의한 컨투어 변동 측정
- **전역 CDU(gCDU)**: 웨이퍼 전체 CD 균일성 변동 측정
- **OPC 오차**: 시뮬레이션된 컨투어와 설계 타겟 간 EPE (MB-OPC 잔류 오차)
- **스캐너 매칭**: 다중 스캐너 간 노광 조건 편차에 의한 EPE
- **SMO 최적화**: V0/M0 레이어의 Source-Mask 동시 최적화로 OPC EPE 최소화

## 검증 지표
- EPE 허용 범위: 5nm 노드 SRAM V0-M0 정렬 기준 — 총 EPE 수 nm 수준
- 스토캐스틱 EPE: 최대 5nm (EUV 공정 기준)
- 시뮬레이터: SMO 최적화 엔진 + 스토캐스틱 리소그래피 시뮬레이터
- 커버리지: 5nm SRAM 실제 공정 데이터 기반

## OPC 툴 구현 관련성
- **EPE 예산 배분 프레임워크**: `VerificationEngine`의 EPE 체크 시 각 기여 요인별 허용 기준을 분리 설정하는 구조 설계에 직접 참조
- OPC 잔류 EPE(OPC Error) 허용 기준 설정 — 5nm 노드 대상 실측 수치 제공
- 스토캐스틱 EPE가 지배적 기여 요인이므로, EUV OPC 검증 시 스토캐스틱 시뮬레이션 통합의 필요성 근거
- SMO와 OPC 검증을 연계한 EPE 최소화 플로우 설계의 기술적 근거

## 참고문헌
- IEEE IITC/MAM 2021
- EPE 관련 선행 연구: "Holistic approach for overlay and EPE to meet 5nm requirements" (SPIE 2018)

## 태그
`Verification`, `IEEE`, `EPE`, `5nm`, `Stochastic`, `SEPE`, `OPCError`, `Overlay`, `SMO`, `EUV`, `EPEBudget`
