# EUV OPC Modeling of Dry Photoresist System for Pitch 32nm BEOL

## 메타데이터
- **저자**: Jyun-Ming Chen, David Rio, Maxence Delorme, Cyrus Tabery, Christoph Hennerkes, Chris Spence, Benjamin Kam, Mohand Brouri, Nader Shamma
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 129530C
- **DOI/URL**: https://doi.org/10.1117/12.3010402

## 핵심 요약
첨단 EUV 패터닝에서 고해상도 공정은 OPC와 결합되어야 한다. 본 논문은 32nm 피치 BEOL 레이어를 대상으로 건식(dry) 포토레지스트 시스템에 대한 EUV OPC 모델링을 연구한다. 기존 습식 레지스트와 다른 건식 레지스트의 독특한 물리적 특성을 OPC 모델에 통합하는 방법을 제시한다.

## 주요 기여
1. **건식 레지스트 EUV OPC 모델**: 습식 레지스트와 다른 건식 레지스트의 리소그래피 거동 모델링
2. **32nm 피치 BEOL 검증**: 차세대 BEOL 배선 피치에서 OPC 모델 정확도 확인
3. **고해상도 공정 + OPC 통합**: 극소 피치 패터닝을 위한 OPC-공정 공동 최적화
4. **건식 레지스트 특성 분석**: 높은 흡수율, 낮은 확산 등 건식 레지스트 고유 특성의 OPC 영향
5. **EUV BEOL 확장성**: EUV 리소그래피의 BEOL 레이어 적용 확장을 위한 OPC 모델 준비

## Recipe/Flow 상세
- **건식 레지스트 EUV OPC 모델링 플로우**:
  1. **건식 레지스트 물리 특성 파악**:
     - 높은 EUV 흡수율 → 더 낮은 광자 수 요구
     - 낮은 분자 확산 → 더 sharp한 LWR(Line Width Roughness)
     - 특유의 stochastic 거동
  2. **캘리브레이션 패턴 설계**:
     - 32nm 피치 line/space, contact, 2D 패턴
     - 건식 레지스트 특성에 민감한 패턴 포함
  3. **EUV 광학 모델 구성**:
     - EUV 특화 효과(shadowing, flare) + 건식 레지스트 모델
     - 건식 레지스트의 현상(development) 특성 모델링
  4. **OPC 모델 캘리브레이션**:
     - SEM 측정 데이터로 건식 레지스트 OPC 모델 피팅
     - 습식 레지스트 대비 다른 캘리브레이션 파라미터 필요
  5. **32nm BEOL OPC 적용 및 검증**:
     - 캘리브레이션된 모델로 BEOL 금속 레이어 OPC 수행
     - 웨이퍼 프린팅 결과로 모델 예측 정확도 검증
- **건식 레지스트 vs. 습식 레지스트**:
  - 건식: 진공 환경 증착, 높은 흡수율, 낮은 확산, 더 좋은 LWR
  - 습식: 스핀 코팅, 익숙한 공정, 더 성숙한 모델
- **BEOL 특화**: M1, M2 등 금속 배선 32nm 피치 목표

## OPC 툴 구현 관련성
- 건식 레지스트 도입 시 SKOPC EUV 레지스트 모델 확장 필요
- `dry_resist_model.py`: 건식 레지스트 특화 현상 모델 구현
- BEOL EUV OPC에서 건식 레지스트 파라미터 분리 처리
- 32nm 이하 피치 BEOL OPC 레시피 설계 기준

## 태그
`EUV`, `DryPhotoresist`, `OPC`, `BEOL`, `32nm`, `ModelBuilding`, `Metal`, `SPIE`, `2024`
