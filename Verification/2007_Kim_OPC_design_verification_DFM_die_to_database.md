# OPC and Design Verification for DFM Using Die-to-Database Inspection

## 메타데이터
- **저자**: JungChan Kim, HyunJo Yang, JooKyoung Song, DongGgyu Yim, JinWoong Kim, Toshiaki Hasebe, Masahiro Yamamoto
- **연도**: 2007
- **게재지**: Proc. SPIE 6521, Design for Manufacturability through Design-Process Integration, 652117
- **DOI/URL**: https://doi.org/10.1117/12.711348

## 핵심 요약
광학 리소그래피 한계에 근접한 공정 환경에서, D2DB(Die-to-Database) 검사 기반 신규 DFM 검증 툴을 이용하여 설계 이슈, OPC 오차, 수차, 공정 변수에 대한 풀칩 데이터 피드백을 구현한 논문. 리소그래피 친화적 설계와 공정 안정성을 확보하기 위해 D2DB 검사 데이터를 OPC 및 설계 최적화에 직접 피드백하는 DFM 통합 플로우를 제시하였다.

## 주요 기여
1. **DFM 통합 검증 툴**: 설계 이슈, OPC 오차, 수차, 공정 변수를 모두 포착하는 통합 DFM 검증 플랫폼
2. **풀칩 D2DB 피드백 루프**: D2DB 검사 데이터를 설계 개선 및 OPC 재최적화에 직접 피드백하는 폐루프 시스템
3. **리소그래피 친화적 설계 지원**: 수율과 공정 안정성을 위한 설계 규칙 준수 여부를 D2DB 방식으로 검증
4. **OPC 오차 및 수차 동시 포착**: 단순 OPC 검증을 넘어 렌즈 수차 효과와 공정 변수 영향을 통합하여 분석
5. **양산 DFM 플로우 통합**: 팹의 양산 OPC 플로우에 통합 가능한 실용적 DFM 검증 방법론

## 검증 방법론
- 신규 DFM D2DB 검증 툴로 풀칩 레이아웃 분석 및 결함 데이터 수집
- 설계 이슈, OPC 오차, 수차 기여별 결함 분류 및 통계
- D2DB 피드백 기반 OPC 재최적화 후 결함 감소 효과 측정
- 기존 검증 방법 대비 신규 DFM 플로우의 결함 포착 완전성(coverage) 비교

## OPC 툴 구현 관련성
- SKOPC의 DFM 통합 검증 기능 설계 시 참조: 단순 OPC 검증을 넘어 수차, 공정 변수를 통합한 포괄적 검증
- `2006_Yang_OPC_verification_die_to_database_inspection.md`(동일 저자 그룹)의 후속 발전 연구로, D2DB 방식을 DFM 전반으로 확장
- SKOPC의 풀칩 OPC 검증 리포트에 수차 기여 및 공정 변수 영향을 포함하는 통합 보고 형식 설계 근거
- `recipes/` 레시피 파일에 수차 파라미터 및 공정 변수 항목 추가 시 검증 필요성 근거 문헌

## 태그
`Verification`, `SPIE`, `DFM`, `OPC`, `Die-to-Database`, `Aberration`, `Process Variation`, `Full Chip`, `Design`, `Manufacturability`
