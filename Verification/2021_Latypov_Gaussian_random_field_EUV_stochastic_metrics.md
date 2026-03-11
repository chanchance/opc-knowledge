# Gaussian Random Field EUV Stochastic Models, Their Generalizations and Lithographically Meaningful Stochastic Metrics

## 메타데이터
- **저자**: Azat Latypov, Gurdaman Khaira, Germain Fenger, Shuling Wang, Marko Chew, Shumay Shang (Siemens Digital Industries Software)
- **연도**: 2021
- **게재지**: Proc. SPIE 11609, Extreme Ultraviolet (EUV) Lithography XII, 1160917
- **DOI/URL**: https://doi.org/10.1117/12.2583792

## 핵심 요약
EUV 리소그래피의 스토캐스틱 현상을 가우시안 랜덤 필드(GRF) 이론으로 모델링하고, 풀칩 OPC 및 검증(verification)에 적용 가능한 리소그래피 의미있는 스토캐스틱 지표(stochastic metrics)를 도출한 논문. 광자 흡수 통계와 레지스트 화학 모델을 통합한 GRF 기반 디프로텍션(deprotection) 모델 계열을 제시하고, 고갈(depletion) 효과와 공정 파라미터 변동을 고려한 확률론적 반응-확산 모델로 일반화하였다.

## 주요 기여
1. **GRF 기반 EUV 스토캐스틱 모델 계열**: 광자 흡수 통계 + 레지스트 화학을 통합한 GRF 디프로텍션 모델 수립
2. **반응-확산 모델로의 일반화**: 레지스트 산(acid) 고갈 효과 및 공정 파라미터 변동을 포함한 확장 모델
3. **리소그래피 의미있는 스토캐스틱 지표 정의**: 리소그래퍼가 실용적으로 활용 가능하고 풀칩 OPC/검증에 빠르게 적용할 수 있는 스토캐스틱 메트릭 체계
4. **풀칩 OPC-검증 통합 적용성**: 계산 효율성을 고려한 지표 설계로 풀칩 시뮬레이션에서 스토캐스틱 검증 가능
5. **Rice 공식 기반 실패 확률 예측**: GRF 이론의 Rice 공식을 활용한 EUV 패터닝 실패 확률 해석적 계산

## 검증 방법론
- GRF 모델 예측 스토캐스틱 지표와 실제 EUV 웨이퍼 측정 데이터 비교 검증
- 기존 결정론적(deterministic) OPC 시뮬레이션 대비 스토캐스틱 모델의 추가 예측력 정량화
- 풀칩 수준에서의 계산 시간 대비 스토캐스틱 지표 정확도 트레이드오프 분석
- 여러 EUV 기술 노드에서 GRF 모델 파라미터 캘리브레이션 및 검증

## OPC 툴 구현 관련성
- SKOPC에서 EUV 스토캐스틱 OPC 검증 기능 구현 시 핵심 이론 기반 문헌
- `2024_Wang_stochastic_OPC_cost_function_EUV.md`, `2019_VaglioPret_OPC_stochastic_EUV_failure_rate.md`와 함께 EUV 스토캐스틱 OPC 이론 계보 구성
- 풀칩 스토캐스틱 검증을 위한 GRF 기반 지표를 SKOPC 검증 리포트 항목으로 추가할 때 정의 기준
- `LithoEngine`의 EUV 스토캐스틱 시뮬레이션 모듈 확장 시 모델 수식 참조

## 태그
`Verification`, `SPIE`, `EUV`, `Stochastic`, `Gaussian Random Field`, `OPC`, `Metrics`, `Resist Model`, `Full Chip`
