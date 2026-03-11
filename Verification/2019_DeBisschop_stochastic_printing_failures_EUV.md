# Stochastic Printing Failures in EUV Lithography

## 메타데이터
- **저자**: P. De Bisschop, E. Hendrickx
- **연도**: 2019
- **게재지**: Proc. SPIE 10957, Extreme Ultraviolet (EUV) Lithography X, 109570E
- **DOI/URL**: https://doi.org/10.1117/12.2515082

## 핵심 요약
EUV 리소그래피에서 스토캐스틱 효과로 인한 인쇄 실패(printing failure)를 체계적으로 연구한 기초 논문. L/S(Line/Space) 또는 컨택/닷 어레이의 SEM 이미지에서 스토캐스틱 인쇄 실패를 감지하는 알고리즘을 개발하고, "NOK(Not OK)" 스토캐스틱 실패 지표를 정의하였다. 이 지표는 이후 EUV 스토캐스틱 OPC 연구의 핵심 검증 메트릭으로 광범위하게 인용되었다.

## 주요 기여
1. **NOK(Not OK) 스토캐스틱 실패 지표 정의**: SEM 이미지 분석 기반으로 L/S 및 컨택/닷 어레이에서 스토캐스틱 인쇄 실패를 정량화하는 NOK 지표 제안
2. **SEM 이미지 기반 자동 감지 알고리즘**: 대규모 SEM 이미지 세트에서 스토캐스틱 인쇄 실패를 자동으로 감지·분류하는 알고리즘
3. **패턴 유형별 실패 분석**: L/S 및 컨택/닷 어레이에서 bridge, break 등 실패 유형별 발생 통계
4. **스토캐스틱 실패율 추출**: 다양한 CD 및 공정 조건에서 스토캐스틱 실패 확률 곡선(failure rate curve) 도출
5. **EUV 스토캐스틱 검증 기준 확립**: 이후 EUV OPC 검증에서 스토캐스틱 성능 평가의 업계 기준 지표 제공

## 검증 방법론
- EUV 노광 웨이퍼의 대규모 SEM 이미지 수집
- 자동 알고리즘으로 SEM 이미지에서 bridge/break 등 NOK 패턴 감지
- CD 및 포커스/도즈 조건별 NOK 발생률 통계 분석
- 결정론적(deterministic) OPC 시뮬레이션과의 비교로 스토캐스틱 기여 분리

## OPC 툴 구현 관련성
- SKOPC의 EUV 스토캐스틱 OPC 검증 기준 지표(NOK metric) 구현의 핵심 원천 논문
- `2019_VaglioPret_OPC_stochastic_EUV_failure_rate.md`, `2021_Latypov_Gaussian_random_field_EUV_stochastic_metrics.md`, `2021_Wang_stochastic_defect_criticality_EUV_yield.md`의 공통 기반 참조 논문
- `2024_Wang_stochastic_OPC_cost_function_EUV.md`(기수집)에서 NOK 지표가 OPC 비용함수로 활용되는 배경 이해에 필수
- SKOPC EUV 스토캐스틱 검증 보고서의 NOK 지표 정의 표준

## 태그
`Verification`, `SPIE`, `EUV`, `Stochastic`, `NOK`, `Printing Failure`, `Bridge`, `Break`, `SEM`, `OPC`
