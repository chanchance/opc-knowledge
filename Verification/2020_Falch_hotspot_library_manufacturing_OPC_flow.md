# Integrating Enhanced Hotspot Library into Manufacturing OPC Correction Flow

## 메타데이터
- **저자**: Bradley J. Falch, Linghui Wu, John Tsai, Elsley Tan, Jiunhau Fu, Tengyen Huang, Chuncheng Liao
- **연도**: 2020
- **게재지**: Proc. SPIE 11328, Design-Process-Technology Co-optimization for Manufacturability XIV, 113280E
- **DOI/URL**: https://doi.org/10.1117/12.2552110

## 핵심 요약
피처 크기 축소와 보정 플로우 복잡성 증가로 인해 OPC 검증에서 항상 일부 실패 hotspot이 발생하는 상황에서, 이러한 hotspot 정보를 표준 OPC 보정 레시피에 통합하는 방법론을 제안한 논문. 패턴 매칭으로 hotspot 영역을 식별하고 표준 레시피 파라미터 또는 보정 기법을 hotspot별로 조정하여, 미래 설계에서 동일 유형 hotspot의 재발을 방지하는 enhanced hotspot 라이브러리 기반 제조 OPC 플로우를 구현하였다.

## 주요 기여
1. **Enhanced Hotspot 라이브러리 구축**: 발견된 OPC 검증 실패 hotspot을 분류하고 레시피 수정 정보와 함께 라이브러리화
2. **패턴 매칭 기반 Hotspot 영역 식별**: 설계 레이아웃에서 라이브러리 hotspot 패턴을 자동으로 매칭하여 위험 영역 식별
3. **표준 OPC 레시피 업데이트**: 식별된 hotspot 영역에 대해 레시피 파라미터 또는 보정 기법을 자동으로 조정
4. **제조 OPC 플로우 통합**: Enhanced hotspot 라이브러리 적용을 표준 제조 OPC 플로우에 매끄럽게 통합
5. **Hotspot 재발 방지**: 라이브러리 기반 사전 보정으로 동일 유형 hotspot의 향후 설계에서의 재발 억제

## 검증 방법론
- 이전 설계에서 발견된 OPC 검증 실패 hotspot으로 라이브러리 구축
- 신규 설계 레이아웃에 패턴 매칭을 적용하여 잠재 hotspot 영역 사전 식별
- Enhanced hotspot 라이브러리 적용 전후 OPC 검증 실패 건수 비교
- 라이브러리 기반 보정 적용 후 웨이퍼 EPE 분포 및 수율 개선 정량화

## OPC 툴 구현 관련성
- SKOPC의 OPC 레시피 시스템에 hotspot 라이브러리 기반 자동 레시피 조정 기능 구현 시 핵심 참조
- `2017_Hamouda_OPC_recipe_coverage_hotspot.md`(기수집)의 레시피 커버리지 분석을 실제 제조 플로우 통합으로 확장
- SKOPC Recipe Runner의 hotspot 인식 자동 파라미터 조정(adaptive recipe) 기능 설계의 기초
- `recipes/example_arfimm.yaml` 등의 레시피 파일에 hotspot 라이브러리 참조 기능 추가 시 참조

## 태그
`Verification`, `SPIE`, `Hotspot`, `OPC Recipe`, `Pattern Matching`, `Manufacturing`, `Yield`, `Library`, `DFM`
