# New OPC Verification Method Using Die-to-Database Inspection

## 메타데이터
- **저자**: Hyunjo Yang, Jaeseung Choi, Byungug Cho, Jongkyun Hong, Jookyoung Song, Donggyu Yim, Jinwoong Kim, Masahiro Yamamoto
- **연도**: 2006
- **게재지**: Proc. SPIE 6152, Metrology, Inspection, and Process Control for Microlithography XX, 615232
- **DOI/URL**: https://doi.org/10.1117/12.656857

## 핵심 요약
웨이퍼 상의 모든 패턴을 원본 레이아웃 데이터베이스(CAD database)와 직접 비교하는 Die-to-Database(D2DB) 검사 방법을 OPC 검증에 적용한 논문. nm 수준 크기의 체계적 결함(systematic defect)을 원본 레이아웃 타겟으로부터 모두 식별하고, 이를 OPC 모델 재튜닝(re-tuning)에 피드백하는 새로운 OPC 검증-보정 루프를 구현하였다.

## 주요 기여
1. **D2DB 기반 OPC 검증 방법론**: 기존 시뮬레이션 기반 검증을 실제 웨이퍼-데이터베이스 직접 비교로 보완하는 새로운 OPC 검증 접근법
2. **nm 수준 체계적 결함 검출**: 기존 방법으로 포착하기 어려운 nm 수준의 체계적 오차를 D2DB 비교로 식별
3. **OPC 모델 피드백 루프**: 발견된 체계적 오차를 OPC 모델 재튜닝에 직접 피드백하는 폐루프(closed-loop) 보정 체계
4. **모든 패턴 유형 검증**: 특정 패턴 선택 없이 웨이퍼 상의 모든 패턴에 대한 포괄적 검증 가능
5. **양산 OPC 품질 관리**: 제조 라인에서 OPC 품질을 지속적으로 모니터링하는 실용적 방법론

## 검증 방법론
- 실제 웨이퍼 이미지(SEM 또는 광학 검사)와 CAD 데이터베이스의 직접 D2DB 비교
- 체계적 결함의 크기 분포 및 패턴 유형별 분류
- D2DB 검증 발견 결함과 OPC 모델 잔차 간의 상관관계 분석
- OPC 모델 재튜닝 후 D2DB 재검증으로 개선 효과 확인

## OPC 툴 구현 관련성
- SKOPC의 OPC 검증 모듈에 D2DB 기반 검증 기능 추가 시 참조
- `2007_Marokkey_validating_OPC_models_masks_wafers.md`의 모델-마스크-웨이퍼 3단계 검증에서 웨이퍼 단계를 D2DB 방법으로 구체화하는 관계
- OPC 모델 자동 재캘리브레이션 루프(실측 피드백) 기능 설계의 기초 문헌
- SKOPC의 풀칩 OPC 검증 리포트에 D2DB 비교 기반 체계적 오차 항목 포함 근거

## 태그
`Verification`, `SPIE`, `OPC`, `Die-to-Database`, `Inspection`, `Systematic Defect`, `Model Feedback`, `CD-SEM`, `Metrology`
