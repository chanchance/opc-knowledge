# Accurate Process Window Determination for EUV Lithography Using Large Field of View eBeam Metrology and Stochastic-Aware Modeling

## 메타데이터
- **저자**: Su-Te Ma, Chih-Ping Chang, Yi-Yi Chen, Yen-Lung Lu, Teng-Yen Huang, Hepeng Ding, Sangyoon Shim, Zehua Han, Franklin Wong, Guanchen He, Selena Chen, Luke Lin, Chih-Hung Hsieh
- **연도**: 2025
- **게재지**: Proc. SPIE 13426, Metrology, Inspection, and Process Control XXXIX, 134262M
- **DOI/URL**: https://doi.org/10.1117/12.3051560
- **소속**: Nanya Technology Corp. (대만), ASML (미국/대만)

## 핵심 요약
EUV 리소그래피의 정확한 공정 윈도우 결정을 위해 대시야각(LFoV) 주사 전자현미경과 확률론적 인식(stochastic-aware) 모델링을 결합한 방법론을 제시한다. DRAM 제조사(Nanya)와 ASML이 협력하여 LFoV SEM + 공정 윈도우 계측 분석 소프트웨어 + 확률적 모델 기반 피처 실패 예측을 통합한 고급 EUV 공정 윈도우 분석 접근법을 구현한다.

## 주요 기여
1. LFoV SEM + 확률적 인식 모델링을 결합한 EUV 공정 윈도우 결정 방법론
2. 피처 실패(feature failure) 예측에 확률적 모델 적용
3. 공정 윈도우 계측 분석 소프트웨어와 LFoV 계측 통합 파이프라인
4. DRAM 제조 환경에서 EUV 공정 윈도우 정밀 결정 실증 (Nanya Technology)
5. 확률적 불균일성(stochastic variability)을 고려한 공정 윈도우 마진 평가

## 검증 방법론
- **계측 방법**: LFoV(Large Field of View) SEM 이미징
- **모델링**: 확률적 인식(stochastic-aware) 컴팩트 모델
- **분석 소프트웨어**: 공정 윈도우 계측 분석 플랫폼 (ASML)
- **예측 대상**: 피처 실패 확률 vs Focus/Dose 조건
- **검증 환경**: DRAM EUV 레이어 (Nanya Technology)
- **결과**: EUV 확률적 불균일성을 반영한 정확한 공정 윈도우 경계 결정

## OPC 툴 구현 관련성
- EUV OPC 검증의 공정 윈도우 분석에 확률적 모델 통합 필요성 실증
- LFoV SEM 데이터를 OPC 공정 윈도우 검증에 활용하는 방법론
- DRAM EUV 레이어에서 확률적 피처 실패 예측을 OPC 핫스팟 분류에 활용
- EUV 공정 윈도우 결정 시 기존 Bossung 커브 대비 확률적 접근의 우수성

## 태그
`Verification`, `EUV`, `ProcessWindow`, `StochasticModeling`, `LFoVMetrology`, `DRAM`, `FeatureFailure`, `SPIE`, `2025`
