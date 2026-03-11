# EPE Budget Analysis and Margin Co-Optimization on the Multiple Critical On-Device Features in a Single Image for Yield Enhancement

## 메타데이터
- **저자**: Yaniv Abramovitz, Boo-Hyun Ham, Sangho Jo, Byoung-Hoon Kim, Jongsu Kim, Insung Kim, Kevin Houchens, Noam Shaham, Jeong Ho Yeo, PavanKumar Mannava
- **연도**: 2021
- **게재지**: Proc. SPIE 11611, Metrology, Inspection, and Process Control for Semiconductor Manufacturing XXXV, 116111Z
- **DOI/URL**: https://doi.org/10.1117/12.2585369

## 핵심 요약
1nm 노드를 향해 축소되는 첨단 로직 노드에서 EUV 리소그래피의 EPE(Edge Placement Error) 제어가 핵심 과제가 된 상황에서, 단일 이미지에서 다수의 임계 온디바이스 피처(on-device feature)에 대한 EPE 예산 분석 및 마진 공동 최적화 방법론을 제안한 논문. CD와 오버레이 오차가 주요 EPE 기여 인자임을 규명하고, 단일 이미지 내 다중 피처의 EPE 예산을 동시에 분석하는 데이터 무결성 확보 방법을 제시하였다.

## 주요 기여
1. **다중 피처 동시 EPE 예산 분석**: 단일 이미지 내 여러 종류의 임계 피처(HS 포함)에 대한 EPE를 동시에 분석하는 방법론
2. **데이터 무결성 문제 해결**: 서로 다른 공정 단계, 계측 툴(SEM, OM), 측정 타겟에서 수집된 데이터의 무결성 보장 방법
3. **CD+오버레이 통합 EPE 예산**: CD 오차와 오버레이 오차를 모두 포함한 통합 EPE 예산 프레임워크
4. **마진 공동 최적화**: 단일 이미지 내 다수 피처의 EPE 마진을 동시에 최적화하는 co-optimization 전략
5. **수율 향상 연계**: EPE 예산 분석과 공정 수율 향상 간의 직접적 연관성 실증

## 검증 방법론
- 단일 이미지 내 다수 임계 피처에 대한 동시 CD-SEM 측정으로 EPE 데이터 취득
- EPE 기여 인자(CD 오차 vs. 오버레이 오차) 분리 분석
- EPE 예산 분석 전후 공정 마진 및 수율 지표 비교
- 기존 단일 피처 EPE 분석 대비 다중 피처 공동 분석의 추가 가치 정량화

## OPC 툴 구현 관련성
- SKOPC의 EPE 분석 및 OPC 검증 보고서에 다중 피처 동시 EPE 예산 분석 기능 추가 시 참조
- `2021_Saha_EPE_variability_multi_patterning_comparison.md`와 함께 EPE 예산 분석 방법론 계보 구성
- SKOPC PWO 모듈에서 여러 임계 피처의 마진을 공동 최적화하는 비용함수 설계에 직접 참조
- EUV 첨단 노드에서 CD+오버레이 통합 EPE 예산 계산 모듈 설계의 기준 논문

## 태그
`Verification`, `SPIE`, `EPE`, `Budget Analysis`, `OPC`, `EUV`, `Overlay`, `CD`, `Yield`, `Co-Optimization`
