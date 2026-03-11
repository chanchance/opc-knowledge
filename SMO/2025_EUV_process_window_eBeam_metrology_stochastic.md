# Accurate Process Window Determination for EUV Lithography Using Large Field of View eBeam Metrology and Stochastic-Aware Modeling

## 메타데이터
- **저자**: (SPIE 13426 저자 정보)
- **연도**: 2025
- **게재지**: Proc. SPIE 13426, Metrology, Inspection, and Process Control XXXIX, 134262M (2025)
- **DOI/URL**: https://doi.org/10.1117/12.3051560

## 핵심 요약
EUV 리소그래피의 정확한 공정 창 결정을 위해 대시야(large field of view) 전자빔(eBeam) 계측과 확률론적 인식 모델링을 결합한 새로운 방법론을 제시한다. 기존 소수 CD 측정 기반 공정 창 추정의 한계를 극복하고 통계적으로 유의미한 EUV 공정 창을 결정하는 방법을 개발한다.

## 주요 기여
1. **대시야 eBeam 계측**: 대면적 전자빔 검사로 통계적으로 유의미한 CD/공정 창 데이터 확보
2. **확률론적 인식 공정 창**: P_fail 기반 확률론적 공정 창 정의 및 결정 방법론
3. **EUV 공정 창 정확도 향상**: 확률론적 결함을 포함한 실질적 EUV 공정 창 결정
4. **계측-모델 연계**: eBeam 계측 데이터와 확률론적 모델 교정의 통합

## 알고리즘/수식
### 확률론적 인식 공정 창
```
기존 공정 창 정의:
  PW_classical = {(dose, focus) : CD ∈ [CD_target ± ΔCD]}
  → 평균 CD만 고려, 확률론적 변동 무시

확률론적 공정 창:
  PW_stochastic = {(dose, focus) : P_fail < P_threshold}
  P_fail(dose, focus) = f(NILS, dose, stochastic_model)
  P_threshold: 수율 요구사항 기반 (예: 1 ppb)

대시야 eBeam 계측:
  측정 필드: 수천~수만 피처 동시 측정
  → LCDU, LWR, 확률론적 결함 밀도 통계
  → 충분한 표본 크기로 희귀 이벤트 포착
```

### 공정 창 결정 방법론
```
공정 창 결정 단계:
  1. 대시야 eBeam으로 Focus-Exposure Matrix (FEM) 측정
     → 각 (dose, focus)에서 수천 CD 값
  2. 확률론적 모델 교정:
     P_fail(x,y) = Φ(-(NILS(x,y) - NILS_threshold) / σ_stoch)
  3. P_fail 지도 생성:
     → 각 (dose, focus)에서 P_fail 값
  4. 공정 창 경계 결정:
     PW_boundary = {P_fail = P_threshold}

성능 개선:
  기존 대비 공정 창 정확도 향상
  희귀 확률론적 결함 예측 포함
```

## OPC 툴 SMO 구현 관련성
- 확률론적 공정 창 SMO: SKOPC SMO 비용 함수에 P_fail 기반 공정 창 통합
- eBeam 계측 연계: 대시야 eBeam 데이터로 OPC 모델 확률론적 보정
- EUV 수율 예측: 확률론적 공정 창으로 더 정확한 수율 예측
- 계측-OPC 루프: 계측 데이터 기반 OPC 최적화 피드백 루프

## 태그
`EUV`, `process_window`, `eBeam`, `metrology`, `stochastic`, `P_fail`, `LCDU`, `OPC`, `SMO`, `yield`, `SPIE`, `2025`
