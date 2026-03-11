# Compact Modeling of Stochastics and Application in OPC

## 메타데이터
- **저자**: Werner Gillijns, Jae-uk Lee, Ryan Ryoung Han Kim, Chih-I Wei, Xima Zhang, Azat Latypov, Germain Fenger, John Sturtevant
- **연도**: 2023
- **게재지**: Proc. SPIE 12494, Optical and EUV Nanolithography XXXVI, 124940J
- **DOI/URL**: https://doi.org/10.1117/12.2658260
- **소속**: imec, Siemens EDA

## 핵심 요약
EUV 리소그래피 도입으로 기존 결정론적(deterministic) OPC 컴팩트 모델의 한계가 드러난 상황에서, 확률적(stochastic) 변동성을 OPC에 통합하는 컴팩트 스토캐스틱 모델 방법론을 제시한다. 이미징 메트릭과 변동성 사이의 경험적 상관관계를 기반으로 개발된 스토캐스틱 모델을 OPC 수행 중에 적용하여 확률적 실패(stochastic failures)를 줄이는 전략을 랜덤 로직 및 SRAM 설계의 비아(via) 레이어에서 검증한다.

## 주요 기여
1. **확률적 컴팩트 모델의 OPC 통합**: 결정론적 OPC 모델의 EUV 한계를 극복하는 스토캐스틱 모델 적용
2. 이미징 메트릭-변동성 경험적 상관관계 기반 컴팩트 스토캐스틱 모델 개발
3. OPC 수행 중 스토캐스틱 모델 적용으로 확률적 실패 감소 전략
4. 랜덤 로직 + SRAM 비아 레이어에서 캘리브레이션된 스토캐스틱 모델로 다양한 OPC 전략 비교
5. 풀칩 OPC 및 검증에 적용 가능한 속도-정확도 균형 컴팩트 모델 프레임워크

## 검증 방법론
- **대상 레이어**: EUV 비아(via) 레이어 (랜덤 로직 + SRAM 설계)
- **모델 유형**: 캘리브레이션된 확률적 컴팩트 모델
- **OPC 전략 비교**: 여러 스토캐스틱 인식 OPC 전략 적용 및 비교
- **평가 지표**: 확률적 실패율 감소 (기존 결정론적 OPC 대비)
- **기반 연구**: 이미징 메트릭-EUV 변동성 경험적 상관관계
- **적용 범위**: 풀칩 OPC 및 검증에 적용 가능한 계산 효율성 확보

## OPC 툴 구현 관련성
- EUV OPC 모델에 스토캐스틱 요소를 통합하는 컴팩트 모델 구현 방법론
- 비아/컨택 레이어의 EUV 확률적 실패를 줄이는 OPC 전략 설계 기준
- 풀칩 OPC 런타임을 유지하면서 스토캐스틱 모델을 적용하는 컴팩트 모델 접근법
- `2021_Latypov_Gaussian_random_field_EUV_stochastic_metrics.md`의 스토캐스틱 메트릭을 OPC에 실제 통합한 후속 연구

## 태그
`Verification`, `EUV`, `StochasticModeling`, `OPCModel`, `CompactModel`, `Via`, `SRAM`, `StochasticFailure`, `imec`, `SPIE`, `2023`
