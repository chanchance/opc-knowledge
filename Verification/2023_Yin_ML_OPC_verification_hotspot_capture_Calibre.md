# Machine Learning Assisted Effective OPC Verification Hotspot Capture

## 메타데이터
- **저자**: Lianghong Yin, Marko Chew, Shumay Shang, Le Hong, Fan Jiang, Ilhami Torunoglu (Siemens EDA)
- **연도**: 2023
- **게재지**: Proc. SPIE 12751, Photomask Technology 2023, 127510W
- **DOI/URL**: https://doi.org/10.1117/12.2687752

## 핵심 요약
Siemens EDA Calibre ML 보조 OPC 검증 툴을 활용하여, 하나의 단일 제약 조건으로 레이아웃 전체에서 모든 종류의 hotspot을 효과적으로 포착하는 혁신적 방법론을 제안한 논문. ML 분류기를 통한 패턴 차별화와 분류 제한 함수를 통한 출력 데이터 볼륨 제어를 결합하여, OPC 검증 레시피 설정 복잡도와 엔지니어링 작업 부하를 크게 감소시키면서도 실제 hotspot 포착 효율을 향상시켰다.

## 주요 기여
1. **단일 제약 조건 멀티-hotspot 포착**: 기존 패턴별 개별 제약 조건 대신 하나의 제약으로 모든 실패 메커니즘 hotspot 포착
2. **ML 분류기 기반 패턴 차별화**: ML 분류기로 레이아웃 패턴을 구분하여 false positive 없이 실제 hotspot만 선별
3. **출력 데이터 볼륨 제어**: 분류 제한 함수를 통해 OPC 검증 결과 데이터 볼륨을 관리 가능한 수준으로 유지
4. **OPC 검증 레시피 단순화**: 복잡한 튜닝 제약 조건 대신 ML 기반 분류로 레시피 설정 엔지니어링 부담 감소
5. **풀칩 레이아웃 적용**: 셀 수준이 아닌 풀칩 레이아웃에 적용 가능한 확장성 확보

## 검증 방법론
- ML 분류기 훈련 데이터: 알려진 hotspot/non-hotspot 패턴 레이블 데이터셋
- 단일 제약 조건 ML 보조 검증과 기존 다중 튜닝 제약 조건 검증의 hotspot 포착률 비교
- False positive/false negative 비율 비교
- 출력 데이터 볼륨 감소율 정량화
- 풀칩 런타임 비교 (ML 보조 vs. 기존 방법)

## OPC 툴 구현 관련성
- SKOPC의 OPC 검증 모듈에 ML 기반 hotspot 분류 기능 통합 시 직접 참조
- `2023_Yin_ML_OPC_verification_hotspot_capture.md`(기수집)와 동일 저자 그룹의 후속/보완 연구 — 기수집 파일이 TCAD 저널 논문이라면 이 논문은 SPIE Photomask 트랙 발표
- `2020_Falch_hotspot_library_manufacturing_OPC_flow.md`의 패턴 라이브러리 방식을 ML로 대체/강화하는 방향성 제시
- SKOPC 검증 레시피 자동화(recipe auto-tuning) 기능의 ML 구현 기준 논문

## 태그
`Verification`, `SPIE`, `Machine Learning`, `OPC`, `Hotspot`, `Calibre`, `Pattern Classification`, `Recipe`, `Full Chip`
