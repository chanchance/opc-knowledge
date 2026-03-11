# Calibration and Verification of a Stochastic Model for EUV Resist

## 메타데이터
- **저자**: Gallatin, G. M. et al. (NIST / imec)
- **연도**: 2012
- **게재지**: Proc. SPIE 8322, Extreme Ultraviolet (EUV) Lithography III
- **DOI/URL**: https://doi.org/10.1117/12.917804
- **인용수**: ~90

## 핵심 요약
EUV 레지스트를 위한 확률론적(stochastic) 모델의 캘리브레이션과 검증 방법론을 제시한다. imec 기준 EUV 레지스트(Shinetsu SEVR140)로부터 250개 이상의 CD 및 LWR(Line Width Roughness) 측정 데이터를 수집하여 캘리브레이션을 수행한다. 광자 샷 노이즈(photon shot noise)와 레지스트 내 화학적 확률론적 과정이 LER/LWR에 미치는 영향을 분리하여 정량화한다.

## 주요 기여
1. EUV 레지스트 확률론적 모델 최초 체계적 캘리브레이션 방법론
2. 광자 샷 노이즈 vs. 레지스트 내재 확률론적 효과 분리 분석
3. >250개 CD + LWR 측정값 기반 통계적 캘리브레이션
4. LER/LWR 예측을 포함하는 시뮬레이션 검증
5. EUV 공정 최적화를 위한 stochastic 모델 활용 가이드

## 모델 수식/아키텍처

**EUV 광자 흡수 (포아송 통계):**
```
P(n photons absorbed) = (μ^n · e^{-μ}) / n!
```
μ = 평균 흡수 광자 수 = dose · absorption_cross_section · volume

**PAG(Photo Acid Generator) 활성화:**
```
P(acid generated | n photons) = 1 - (1 - η)^n
```
η = 단일 광자 당 산 생성 확률 (quantum yield)

**산 확산 (확률론적 random walk):**
```
x(t) = x₀ + √(2D·t) · N(0,1)
```
D = 확산계수, 각 산 분자 독립적 확률 이동

**현상 문턱 (stochastic threshold):**
```
resist_edge: [acid concentration](x) ≥ C_th + δ(x)
```
δ(x) ~ N(0, σ_threshold²): 위치별 임계값 변동

**LWR 파워 스펙트럼 밀도:**
```
PSD_LWR(f) = ∫ ⟨δr(0)·δr(x)⟩ · e^{-i2πfx} dx
```

**캘리브레이션 목적함수:**
```
min_{η,D,C_th,σ_th} [||CD_sim - CD_meas||² + α·||LWR_sim - LWR_meas||²]
```

## 모델 유형
- [ ] 광학 모델
- [x] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- EUV OPC 모델 구현 시 결정론적 모델 외 확률론적 항 추가 필요
- LER/LWR 예측은 EUV 공정 윈도우 최적화에 직결
- skopc/modeling/stochastic/ 구현 참조
- 캘리브레이션 데이터: CD(1D 라인/스페이스) + LWR 측정 모두 필요
- Photon shot noise는 dose의 제곱근에 반비례: σ_shot ∝ 1/√dose

## 참고문헌
- Mack, C.A., "Stochastic modeling of photoresist development" (2008)
- Gallatin, G.M., "Resist blur and line edge roughness" (2005)
- Gao, P. et al., "Stochastic model for EUV resist" (2012)

## 태그
`Model`, `SPIE`, `EUV`, `StochasticModel`, `ResistModel`, `LER`, `LWR`, `PhotonShotNoise`, `Calibration`, `2012`
