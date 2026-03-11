# Stochastic-Aware Compact OPC Model Validation for Reducing Failure Probability

## 메타데이터
- **저자**: Werner Gillijns, Jae-uk Lee, Ryan Ryoung-han Kim, Chih-I Wei, Xima Zhang, Azat Latypov, Germain Fenger, John Sturtevant (imec / Siemens Digital Industries Software)
- **연도**: 2025
- **게재지**: SPIE Photomask Japan (PMJ) 2025
- **DOI/URL**: https://doi.org/10.1117/12.3xxx (PMJ 2025 proceedings)

## 핵심 요약
EUV 리소그래피의 stochastic 결함을 수십~수백 배 감소시키는 stochastic-aware Calibre OPC 전략의 웨이퍼 수준 실험 검증 결과를 제시한다. 2022년 GRF 모델 캘리브레이션, 2023년 compact stochastic OPC 적용에 이어, 이 논문은 wafer-level CDSEM 데이터를 통해 stochastic-aware OPC 전략이 실제로 stochastic 결함 확률을 최소 1~2 오더(order) 이상 감소시킴을 실험적으로 입증한다. 이 연구는 5년 이상의 Siemens-imec 공동 연구 시리즈의 최종 단계이다.

## 주요 기여
1. **웨이퍼 수준 stochastic OPC 검증**: 시뮬레이션 예측을 넘어 실제 웨이퍼 CDSEM 데이터로 stochastic-aware OPC 효과 입증
2. **1~2 오더 결함 확률 감소**: 기존 결정론적(deterministic) OPC 대비 stochastic 결함 확률 10~100배 이상 감소 달성
3. **예측-실측 일치**: stochastic 결함 확률 예측값과 실측 CDSEM 데이터의 정량적 일치 확인
4. **다양한 리소그래피 조건 검증**: 다양한 dose, focus 조건에서 stochastic-aware OPC 강건성 검증
5. **Siemens Calibre 플랫폼 생산 적용**: 업계 표준 OPC 툴에서 stochastic-aware 전략 완전 통합

## Recipe/Flow 상세
- **Stochastic-Aware OPC 웨이퍼 검증 플로우**:
  1. **Stochastic 모델 기반 (선행 연구)**:
     - 2022년: GRF(Gaussian Random Field) 모델 캘리브레이션 (LER/LWR/PSD 기반)
     - 2023년: Compact stochastic 모델 → Calibre OPC 적용 ("Compact modeling of stochastics and application in OPC")
     - 모델 파라미터: 공간 상관 길이, 분산, 스펙트럼 형태
  2. **Stochastic-Aware OPC 전략**:
     - 결정론적 OPC: EPE 최소화 목적함수
     - Stochastic-aware OPC: EPE + stochastic 결함 확률 복합 목적함수
     - EPE를 약간 희생하여 stochastic 결함 확률 대폭 감소
     - Via/컨택 레이어에서 stochastic 결함(브리지, 단선) 최소화
  3. **웨이퍼 실험 설계**:
     - 표준 OPC vs. stochastic-aware OPC 동일 웨이퍼 비교
     - EUV via/컨택 레이어 타겟 패턴 설계
     - 다양한 dose/focus 조건 (Focus-Exposure Matrix)
  4. **CDSEM 기반 결함 측정**:
     - 웨이퍼 CDSEM으로 대면적 stochastic 결함 측정
     - 결함 유형 분류: 브리지(bridge), 단선(break), CD 이상
     - 결함 확률 = 결함 개수 / 전체 피처 수
  5. **예측-실측 비교 및 검증**:
     - Calibre stochastic 모델 예측 결함 확률 vs. CDSEM 실측 결함 확률
     - 다양한 리소그래피 조건에서 정량적 일치 확인
     - Stochastic-aware OPC 적용 후 결함 확률 1~2 오더 감소 확인
- **연구 시리즈 (3단계)**:
  - 1단계 (2022): GRF 캘리브레이션 (LER/LWR/PSD 기반 파라미터 추출)
  - 2단계 (2023): Compact stochastic 모델 OPC 적용 (SPIE 12494)
  - 3단계 (2025): 웨이퍼 수준 실험 검증 및 생산 적합성 입증 (PMJ 2025)
- **소속 기관**: imec (벨기에) + Siemens Digital Industries Software (미국)

## OPC 툴 구현 관련성
- SKOPC stochastic-aware OPC 모듈의 최종 검증 기준 제공
- `stochastic_aware_opc.py`: GRF 모델 기반 결함 확률 예측 + OPC 목적함수 통합
- 웨이퍼 수준 stochastic OPC 효과 검증 방법론 (CDSEM 비교 프로토콜)
- EUV via/컨택 레이어 stochastic 결함 최소화 OPC 레시피 설계 근거

## 태그
`EUV`, `Stochastic`, `OPC`, `WaferValidation`, `GaussianRandomField`, `FailureProbability`, `CDSEM`, `Calibre`, `Siemens`, `imec`, `Via`, `Contact`, `PMJ`, `2025`
