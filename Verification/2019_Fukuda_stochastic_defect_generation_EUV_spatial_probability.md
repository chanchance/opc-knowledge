# Stochastic Defect Generation in EUV Lithography Analyzed by Spatially Correlated Probability Model, Reaction-Limited and Scattering-Limited?

## 메타데이터
- **저자**: Hiroshi Fukuda
- **연도**: 2019
- **게재지**: Proc. SPIE 11147, International Conference on Extreme Ultraviolet Lithography 2019, 1114716
- **DOI/URL**: https://doi.org/10.1117/12.2535663

## 핵심 요약
EUV 리소그래피에서 스토캐스틱 패턴 결함 발생 확률이 피처 크기 축소에 따라 지수적으로 증가하는 현상을 설명하는 공간 상관 확률(spatially correlated probability) 모델을 제안한 논문. 몬테카를로 결과에 기반한 기존 확률 모델을 폴리머 크기 이상의 상관관계를 포함하도록 확장하였으며, 실험 결과의 지수적 의존성을 재현하는 정량적 모델 피팅을 수행하였다.

## 주요 기여
1. **공간 상관 확률 모델 개발**: 폴리머 크기를 초과하는 장거리 상관 반응을 포함한 스토캐스틱 결함 확률 모델 제안
2. **지수적 결함 의존성 재현**: 피처 크기 및 dose-to-size에 대한 결함 확률의 실험적 지수적 의존성을 모델로 정량 재현
3. **반응 제한(Reaction-Limited) vs. 산란 제한(Scattering-Limited) 분석**: 두 가지 결함 생성 메커니즘의 상대적 기여를 분리 분석
4. **물리적 파라미터 기반 캘리브레이션**: 실제 물성 범위 내의 재료 파라미터로 모델을 실험 데이터에 정량적으로 피팅
5. **EUV 스토캐스틱 결함 이론적 기반 강화**: 확률론적 반응-확산 모델의 이론적 기반을 공간 상관 효과로 확장

## 검증 방법론
- 몬테카를로 시뮬레이션 기반 스토캐스틱 결함 확률 계산
- 공간 상관 확률 모델의 해석적 표현 도출
- 실험적으로 보고된 결함 확률의 피처 크기 및 도즈 의존성과 모델 예측 비교
- 재료 파라미터(흡수 단면적, 산 확산 길이 등)의 실용적 범위 내에서 모델 피팅

## OPC 툴 구현 관련성
- SKOPC EUV 스토캐스틱 OPC 검증 모듈의 결함 생성 이론 기반 논문
- `2021_Latypov_Gaussian_random_field_EUV_stochastic_metrics.md`의 GRF 모델과 상보적: 이 논문은 결함 생성 물리 메커니즘, Latypov는 시스템 수준 통계 지표
- `2019_DeBisschop_stochastic_printing_failures_EUV.md`의 실험적 NOK 지표와 연계하여 결함 발생 물리 이해
- EUV 스토캐스틱 OPC 비용함수 설계 시 결함 확률의 피처 크기 의존성 모델로 참조

## 태그
`Verification`, `SPIE`, `EUV`, `Stochastic`, `Defect Generation`, `Probability Model`, `Spatial Correlation`, `Monte Carlo`, `OPC`
