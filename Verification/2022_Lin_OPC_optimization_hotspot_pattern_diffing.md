# OPC Optimization and Hotspot Detection Using Pattern Diffing

## 메타데이터
- **저자**: Tsung-Wei Lin, Chun Yen Liu, Hung-Yu Lin, Mang-Shiun Chiang, Jason Sweis, Philippe Hurat, Chun Yen Liao, Chun-Sheng Wu, Chao-Yi Huang, Ya-Chieh Lai
- **연도**: 2022
- **게재지**: Proc. SPIE 12052, DTCO and Computational Patterning, 120521E
- **DOI/URL**: https://doi.org/10.1117/12.2612476

## 핵심 요약
Cadence Pegasus CPA(Computational Pattern Analytics) 기술을 활용하여 레이아웃에서 포괄적인 패턴 뱅크(pattern bank)를 추출하고, 이를 비교(diffing)함으로써 이전에 처리되지 않은 신규 패턴을 효율적으로 발견하는 OPC 최적화 및 hotspot 검출 방법론을 제안한 논문. 전체 칩 시뮬레이션 대신 신규 패턴만 분석함으로써 OPC 엔지니어링 효율을 대폭 향상시키고 수율 경험 이력(history)을 누적하는 패턴 라이브러리 기반 접근법을 제시하였다.

## 주요 기여
1. **Pattern Diffing 방법론**: 설계별 패턴 뱅크를 구축하고 기존 패턴 대비 신규 패턴을 자동으로 식별(diffing)하는 체계
2. **OPC 분석 집중화**: 전체 칩 시뮬레이션 대신 신규 패턴에만 OPC 분석을 집중하여 엔지니어링 효율 향상
3. **패턴 뱅크 이력 관리**: 시간에 따른 패턴 뱅크를 누적 관리하여 수율 경험 데이터베이스 구축
4. **Cadence Pegasus CPA 통합**: 상용 CPA 플랫폼과의 통합을 통한 실용적 구현
5. **OPC 엔지니어 작업 부하 감소**: 신규 패턴 중심 검토로 반복적 전체 칩 시뮬레이션 부담 감소

## 검증 방법론
- 다수의 설계 레이아웃에서 패턴 뱅크 추출 및 diffing 결과의 신규 패턴 발견율 측정
- 패턴 diffing 기반 선별 시뮬레이션과 전체 칩 시뮬레이션의 hotspot 포착률 비교
- 엔지니어링 런타임 비교: 패턴 diffing 기반 vs. 전체 칩 시뮬레이션
- 패턴 뱅크 이력 축적에 따른 신규 패턴 비율 감소 추이 분석

## OPC 툴 구현 관련성
- SKOPC의 OPC 검증 모듈에 패턴 뱅크 기반 incremental 검증 기능 추가 시 핵심 참조
- `2020_Falch_hotspot_library_manufacturing_OPC_flow.md`의 hotspot 라이브러리 방식과 상호 보완: Falch는 hotspot 수정 레시피 라이브러리, 이 논문은 패턴 비교(diffing) 기반 신규 hotspot 발견
- SKOPC Recipe Runner에서 설계 재사용 시 변경된 패턴만 재검증하는 incremental OPC 검증 기능 구현 근거
- `2023_Yin_ML_OPC_verification_hotspot_capture_Calibre.md`의 ML 분류 방식과 함께 사용하면 더 효율적인 두 단계 hotspot 검출 파이프라인 구성 가능

## 태그
`Verification`, `SPIE`, `OPC`, `Hotspot`, `Pattern Diffing`, `Pattern Bank`, `CPA`, `Cadence`, `Full Chip`, `Incremental`
