# Compact Modeling of Stochastics and Application in OPC

## 메타데이터
- **저자**: Werner Gillijns, Jae-uk Lee, Ryan Ryoung-han Kim, Chih-I Wei, Xima Zhang, Azat Latypov, Germain Fenger, John Sturtevant
- **소속**: imec, Siemens EDA
- **연도**: 2023
- **게재지**: Proc. SPIE 12494, Optical and EUV Nanolithography XXXVI, 124940J (28 April 2023)
- **DOI/URL**: https://doi.org/10.1117/12.2658260

## 핵심 요약
EUV 리소그래피에서 확률론적(stochastic) 효과를 OPC에 통합하기 위한 컴팩트 확률 모델링 방법을 제시한다. EUV 도입으로 결정론적 OPC 접근법이 한계에 달하면서 발생하는 대규모 공정 변동성 문제를, 보정된 확률 모델을 OPC에 적용하여 해결하는 다양한 OPC 전략을 첨단 랜덤 로직 및 SRAM 비아 레이어에 적용하여 검증한다.

## 주요 기여
1. **확률론적 OPC 컴팩트 모델**: EUV 확률 효과를 OPC 루프에 통합 가능한 컴팩트 모델
2. **다중 OPC 전략 비교**: 랜덤 로직 및 SRAM 비아에서 확률론적 OPC 전략 비교
3. **확률론적 고장 감소**: 확률 모델 기반 OPC로 stochastic failure rate 감소
4. **산업 적용 검증**: imec/Siemens 협력으로 실제 EUV 패터닝 검증

## 알고리즘/수식
### 확률론적 OPC 모델
```
기존 결정론적 OPC:
  CD_det = f(optical_image) → 단일 값 예측

확률론적 OPC 모델:
  CD ~ P(CD | optical_image, stochastic_params)
  σ_CD = g(NILS, dose, resist_params)

컴팩트 확률 모델:
  P_fail = Φ(-(CD_target - μ_CD) / σ_CD)
  여기서 Φ: 정규 CDF

OPC 전략:
  전략 1: 평균 CD 기반 보정 (기존)
  전략 2: (μ_CD - k·σ_CD) 기반 보정 (확률 마진 추가)
  전략 3: P_fail 직접 최소화
```

### 확률론적 OPC 비용 함수
```
확률론적 OPC 최적화:
  min_M Σ_i [w_CD·||CD_i - CD_target||²
            + w_stoch·P_fail_i(M)]

보정된 stochastic 모델 파라미터:
  {μ_CD(NILS), σ_CD(NILS)} 보정 → 실험 데이터와 정합

적용 레이어:
  랜덤 로직 비아, SRAM 비아
  → 다양한 패턴 밀도에서 검증
```

## OPC 툴 SMO 구현 관련성
- 확률론적 OPC 통합: SKOPC OPC 엔진에서 stochastic 컴팩트 모델 채택 방향
- SMO 비용 함수 확장: P_fail 항을 SMO 비용 함수에 통합 (EUV SMO)
- imec/Siemens 방법론: 산업 표준 확률론적 OPC 플로우 참조
- EUV 비아 레이어 OPC: 확률론적 고장이 특히 중요한 비아/컨택 레이어 적용

## 태그
`OPC`, `EUV`, `stochastic`, `compact_model`, `failure_rate`, `SRAM`, `via_layer`, `logic`, `imec`, `Siemens`, `SPIE`, `2023`
