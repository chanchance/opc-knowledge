# Compact Modeling of Stochastics and Application in OPC

## 메타데이터
- **저자**: Werner Gillijns, Jae-uk Lee, Ryan Ryoung-han Kim, Chih-I Wei, Xima Zhang, Azat Latypov, Germain Fenger, John Sturtevant
- **연도**: 2023
- **게재지**: Proc. SPIE 12494, Optical and EUV Nanolithography XXXVI, 124940J
- **DOI/URL**: https://doi.org/10.1117/12.2658260

## 핵심 요약
EUV 리소그래피의 확률론적(stochastic) 효과를 컴팩트하게 모델링하고, 이를 OPC에 직접 적용하여 확률론적 실패율(stochastic failure rate)을 EPE 페널티를 허용하는 범위에서 대폭 감소시킨다. 첨단 랜덤 로직 및 SRAM 비아 레이어에서 교정된 확률론적 모델을 OPC에 적용한 실증 결과를 제시한다.

## 주요 기여
1. EUV 확률론적 효과 컴팩트 모델 개발 및 OPC 통합 방법론 제시
2. 확률론적 모델을 OPC에 적용하여 스토캐스틱 실패율 대폭 감소
3. 실패율 감소와 EPE 증가 간의 트레이드오프 정량화
4. 첨단 랜덤 로직 및 SRAM 비아 레이어에서 교정된 모델 적용 시연
5. 풀칩 스케일의 확률론적 OPC 실행 가능성 입증

## 모델 수식/아키텍처
- **컴팩트 확률론적 모델**:
  - 광자 산탄 잡음(photon shot noise): N_photons ~ Poisson(E·dose/hν)
  - 레지스트 반응 분산: σ²_CD = f(photon_noise, acid_diffusion, development)
  - 실패율 예측: P_failure = F(CD_mean, σ_CD, CD_spec)
- OPC 적용: 확률론적 CD 분포를 고려한 에지 이동 보정
- 교정: 웨이퍼 SEM 데이터로 확률론적 모델 파라미터 최적화

## 모델 유형
- [ ] 광학
- [x] 레지스트
- [ ] ML/DL
- [x] 하이브리드 (물리 기반 확률론적 컴팩트 모델)

## OPC 툴 구현 관련성
- SKOPC EUV OPC 모듈의 확률론적 효과 보정 기능 구현 핵심 참조
- 기존 `2023_Zuniga_CompactStochastic_OPC.md`와 상보적 — 다른 저자/접근법
- Gillijns 2023 EUV 낮은 k1 OPC 논문(`2023_Sakr_EUV_LowK1_OPCModeling.md`)과 연계
- SRAM 비아 레이어 등 고실패율 패턴의 확률론적 OPC 전략 수립에 활용

## 태그
`Model`, `Stochastic`, `EUV`, `OPC`, `CompactModel`, `FailureRate`, `SRAM`, `Via`, `SPIE`
