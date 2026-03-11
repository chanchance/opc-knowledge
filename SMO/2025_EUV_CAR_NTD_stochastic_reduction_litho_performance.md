# Exploring Stochastic Reduction and Lithographic Performance by Using EUV CAR-NTD

## 메타데이터
- **저자**: (SPIE 13428 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13428, Advances in Patterning Materials and Processes XLII, 134280I (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3050920

## 핵심 요약
EUV 리소그래피에서 CAR-NTD(Chemical Amplified Resist - Non-Thermal Development) 레지스트를 사용한 확률론적 효과 감소와 리소그래피 성능 향상을 탐구한다. 기존 열 현상 기반 CAR 대비 비열 현상 CAR의 LCDU, LWR 특성 개선 효과와 이를 통한 EUV 패터닝 수율 향상을 분석한다.

## 주요 기여
1. **CAR-NTD 확률론적 특성**: 비열 현상 CAR의 낮은 LCDU/LWR로 확률론적 효과 감소
2. **EUV 패터닝 성능**: CAR-NTD 적용 시 EUV 리소그래피 성능 향상 데이터
3. **OPC 모델 적합성**: CAR-NTD 특성에 맞는 OPC 모델 보정 방법론
4. **수율 영향**: 확률론적 결함 감소에 따른 EUV 패터닝 수율 개선 평가

## 알고리즘/수식
### CAR-NTD 레지스트 특성
```
CAR (Chemical Amplified Resist):
  기존 CAR: 열 현상 (thermal development)
    - 현상 시 열 에너지로 화학 반응
    - 잔류 변동 → 확률론적 효과

  CAR-NTD (Non-Thermal Development):
    - 비열 현상 메커니즘
    - 더 균일한 현상 → LCDU 감소
    - LWR 개선

확률론적 개선:
  LCDU_NTD < LCDU_thermal
  LWR_NTD < LWR_thermal
  → P_fail_NTD < P_fail_thermal (동일 도즈)
  → 더 낮은 도즈에서 stochastic 요구사항 충족
```

### OPC 모델 보정
```
CAR-NTD OPC 모델:
  표준 CAR 모델 구조 유지
  현상 모델 파라미터 조정:
    k_develop → k_NTD (비열 현상 계수)
    threshold_NTD ≠ threshold_thermal

  보정 데이터:
    NTD 레지스트로 측정한 CD/LWR 데이터
    → 레지스트 특화 OPC 모델 보정

성능 이점:
  더 낮은 도즈 가능 → 처리량 향상
  더 낮은 LCDU → 패터닝 수율 향상
  OPC 보정 여유(margin) 증가
```

## OPC 툴 SMO 구현 관련성
- CAR-NTD OPC 모델: SKOPC에서 CAR-NTD 레지스트 특성 지원하는 OPC 모델
- 확률론적 OPC 개선: NTD 레지스트의 낮은 LCDU로 확률론적 OPC 요구사항 완화
- 레지스트 타입 확장: 습식/건식/MOR/CAR-NTD 등 다양한 레지스트 모델 지원
- SMO 도즈 최적화: NTD 레지스트의 향상된 감도로 SMO 도즈 목표 조정

## 태그
`EUV`, `CAR`, `NTD`, `non_thermal_development`, `stochastic`, `LCDU`, `LWR`, `OPC`, `resist`, `yield`, `SPIE`, `2025`
