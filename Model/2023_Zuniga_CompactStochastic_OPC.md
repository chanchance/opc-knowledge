# Compact Modeling of Stochastics and Application in OPC

## 메타데이터
- **저자**: Zuniga, C. et al. (Siemens EDA / imec)
- **연도**: 2023
- **게재지**: Proc. SPIE 12494, Optical and EUV Nanolithography XXXVI
- **DOI/URL**: https://doi.org/10.1117/12.2658260
- **인용수**: ~20

## 핵심 요약
EUV 리소그래피의 대규모 변동성이 결정론적 접근법을 무력화하는 문제를 해결하기 위해, 이미징 메트릭과 공정 변동 밴드(process variation band)를 활용한 컴팩트 확률론적 모델을 제안한다. 캘리브레이션된 확률론적 모델로 OPC 보정 시 첨단 랜덤 로직 및 SRAM 설계의 비아 레이어에서 확률론적 실패 수를 저감하는 다양한 OPC 전략을 적용·비교한다.

## 주요 기여
1. OPC 적용 가능한 컴팩트 확률론적 모델 수립 (리고러스 MC 대비 수천 배 빠름)
2. 이미징 메트릭 기반 공정 변동 밴드(PVBand)를 확률론적 OPC 비용함수에 통합
3. 캘리브레이션된 확률론적 모델로 EUV 비아 레이어 실패율 저감 전략 비교
4. 랜덤 로직 + SRAM 설계 전체 셀에서 확률론적 OPC 적용 가능성 실증
5. 결정론적 OPC와 확률론적 OPC의 패터닝 품질 트레이드오프 분석

## 모델 수식/아키텍처

**컴팩트 확률론적 모델 (경험적 상관관계 기반):**
```
P_fail(pattern) = f(NILS, PVBand, local_CD, dose_margin)
```
NILS = Normalized Image Log-Slope (이미징 품질 지표)
PVBand = 공정 변동 밴드 (포커스/도즈 변동 시 CD 변동 범위)

**PVBand 기반 확률론적 실패 추정:**
```
P_fail ≈ Φ(-NILS / σ_stochastic)
σ_stochastic = f(photon_count, resist_blur, ...)
```
Φ = 정규 누적분포함수

**컴팩트 모델 캘리브레이션:**
```
P_fail_compact(NILS, PVBand) ≈ P_fail_rigorous (리고러스 MC 기준)
캘리브레이션: 리고러스 P_fail 계산 → 컴팩트 모델 파라미터 피팅
```

**확률론적 OPC 비용함수:**
```
Cost_stoch = Σ_segments [w_EPE · EPE² + w_Pfail · P_fail + w_CD · ΔCD²]
```
→ 기존 결정론적 EPE만 최소화하는 OPC 대비 확률론적 실패 항 추가

**OPC 전략 비교:**
```
Strategy A: Nominal CD OPC (결정론적)
Strategy B: CD bias 증가 OPC (Pfail 감소 목적)
Strategy C: SRAF 추가 + bias OPC
Strategy D: 확률론적 비용함수 OPC (Pfail 직접 최소화)
```

## 모델 유형
- [ ] 광학 모델
- [x] 레지스트 모델 (컴팩트 확률론적)
- [ ] ML/DL
- [x] 하이브리드 (경험적 상관관계 + 물리 기반 이미징 메트릭)

## OPC 툴 구현 관련성
- EUV OPC 비용함수에 P_fail 항 추가하는 직접적 구현 참조
- skopc/modeling/stochastic_compact.py: NILS/PVBand → P_fail 매핑 구현
- 리고러스 MC 대비 수천 배 빠른 컴팩트 모델로 전체 칩 확률론적 OPC 가능
- 캘리브레이션: 리고러스 모델의 P_fail 계산 결과를 컴팩트 모델 학습 데이터로 활용
- Siemens Calibre의 stochastic OPC 기능 이론적 기반

## 참고문헌
- Gao, W. et al., "OPC strategies to reduce EUV failure rates" (2019)
- Gallatin, G.M. et al., "Calibration of stochastic EUV resist model" (2012)
- Gao, P. et al., "Stochastic model for EUV resist" (2012)

## 태그
`Model`, `SPIE`, `EUV`, `StochasticModel`, `CompactModel`, `OPC`, `FailureRate`, `PVBand`, `NILS`, `2023`
