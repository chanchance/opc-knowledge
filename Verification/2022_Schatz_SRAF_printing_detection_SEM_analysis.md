# Automated SRAF Printing Detection and Quantification Through SEM Image Analysis

## 메타데이터
- **저자**: Jirka Schatz, Francois Weisbuch, Nivea Schuch, Frederic Robert, Thiago Figueiro
- **연도**: 2022
- **게재지**: Proc. SPIE PC12053, Metrology, Inspection, and Process Control XXXVI, PC120530Q
- **DOI/URL**: https://doi.org/10.1117/12.2614732

## 핵심 요약
OPC 플로우의 핵심 구성 요소인 SRAF(Sub-Resolution Assist Feature)가 의도치 않게 레지스트에 인쇄되는 현상(SRAF printing)을 SEM 이미지 분석을 통해 자동으로 감지하고 정량화하는 방법론을 제안한 논문. SRAF 인쇄는 제품 수율을 저하시키는 주요 패터닝 실패 원인 중 하나로, 자동화된 SEM 기반 감지 시스템을 통해 OPC 검증 신뢰도를 높였다.

## 주요 기여
1. **자동화 SRAF 인쇄 감지 시스템**: SEM 이미지를 자동으로 분석하여 SRAF 인쇄 여부를 판별하는 알고리즘
2. **SRAF 인쇄 정량화**: 단순 감지를 넘어 인쇄된 SRAF의 크기, 형태, 심각도를 정량적으로 측정
3. **OPC 검증 루프 통합**: SEM 이미지 분석 기반 SRAF 인쇄 감지를 OPC 검증 플로우에 통합하는 방법론
4. **수율 영향 연계**: SRAF 인쇄 발생 조건과 제품 수율 영향 간의 상관관계 분석
5. **대용량 처리 자동화**: 수동 검토 없이 대량의 SEM 이미지에서 SRAF 인쇄를 자동 분류

## 검증 방법론
- SRAF 인쇄 포함/미포함 SEM 이미지 데이터셋 구축 및 알고리즘 훈련
- 자동 감지 시스템의 감지율(recall) 및 false positive 비율 측정
- 다양한 SRAF 크기/피치 조건에서 감지 성능 평가
- 시뮬레이션 기반 SRAF 인쇄 예측과 SEM 실측 결과 비교 검증

## OPC 툴 구현 관련성
- SKOPC의 SRAF 배치 검증 모듈에서 SRAF 인쇄 위험 패턴 자동 식별 기능 설계 시 참조
- OPC 검증 리포트에 SRAF 인쇄 위험도를 포함하는 SRAF-aware 검증 기준 정의
- `2007_Lee_LRC_process_window_error_detection.md`(기수집)의 LRC 기반 SRAF 검증을 SEM 이미지 분석으로 보완하는 관계
- SKOPC의 post-OPC 시뮬레이션 기반 SRAF 인쇄 예측 모듈 구현에 검증 데이터 기준 제공

## 태그
`Verification`, `SPIE`, `SRAF`, `SEM`, `OPC`, `Printing Detection`, `Yield`, `Image Analysis`, `Metrology`
