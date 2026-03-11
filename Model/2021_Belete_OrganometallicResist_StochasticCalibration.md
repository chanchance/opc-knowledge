# Stochastic Simulation and Calibration of Organometallic Photoresists for Extreme Ultraviolet Lithography

## 메타데이터
- **저자**: Belete, Z., De Bisschop, P., Welling, U., Erdmann, A. (Fraunhofer IISB / imec)
- **연도**: 2021
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology, Vol. 20, No. 1
- **DOI/URL**: https://doi.org/10.1117/1.JMM.20.1.014801
- **인용수**: ~35

## 핵심 요약
EUV 리소그래피 대안 재료인 유기금속(organometallic) 포토레지스트(Inpria-YA)의 확률론적 시뮬레이션 모델을 개발하고 캘리브레이션한다. 집적(aggregation) 기반 현상 메커니즘을 반영한 확률론적 현상 모델을 전체 레지스트 공정 단계에 통합하고, EUV 노광 조건에서의 LER/LWR 예측 및 캘리브레이션 결과를 제시한다.

## 주요 기여
1. 유기금속 레지스트(Inpria-YA) 특화 확률론적 현상 모델 (집적 메커니즘)
2. 전통 CAR(화학증폭레지스트) 대비 유기금속 레지스트의 다른 확률론적 거동 규명
3. EUV 노광 조건(파장 13.5nm)에서의 캘리브레이션 절차 정립
4. LER/LWR, CD 균일도 동시 예측하는 통합 확률론적 모델
5. 유기금속 레지스트의 감도(sensitivity)와 확률론적 효과의 트레이드오프 분석

## 모델 수식/아키텍처

**EUV 광자 흡수 (유기금속):**
```
P(absorption at x) = σ_abs · N_metal · I_EUV(x)
```
σ_abs = 금속(Hf, Sn 등)의 EUV 흡광 단면적 (CAR 대비 훨씬 큼)
N_metal = 단위 부피당 금속 원자 수

**집적 기반 현상 모델:**
```
P(dissolve | x) = f(n_activated_neighbors(x), threshold_N)
```
n_activated = 활성화된 인접 금속 클러스터 수
threshold_N = 현상 문턱 (집적 임계값)

**확률론적 현상 시뮬레이션 (MC):**
```
For each voxel (x,y,z):
  n_photons ~ Poisson(μ(x,y,z))
  activated = (n_photons ≥ n_threshold)
  dissolve = all_neighbors_activated(x,y,z)
```

**LER 파워 스펙트럼:**
```
PSD_LER(f) = |FFT[edge_position(x)]|² / L
```
캘리브레이션: 시뮬레이션 PSD ≈ 측정 PSD

**유기금속 vs. CAR 비교:**
```
CAR: 광자 → 산(H⁺) → 확산 → 탈보호 → 현상  [다단계, 블러 큼]
Organometallic: 광자 → 금속 활성화 → 집적 → 현상  [단순, 블러 작음]
→ 유기금속: 더 작은 σ_blur → 더 낮은 LER 가능성
```

## 모델 유형
- [ ] 광학 모델
- [x] 레지스트 모델 (유기금속 확률론적 모델)
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- 차세대 EUV 레지스트(유기금속)로 전환 시 OPC 모델 재캘리브레이션 필요
- skopc 유기금속 레지스트 모듈: 집적 기반 현상 모델 구현
- 캘리브레이션 데이터: EUV 노광 CD + LER 동시 측정
- 유기금속 레지스트: CAR 대비 γ(감마, 콘트라스트) 높음 → OPC 모델 파라미터 상이
- 높은 금속 흡광 단면적 → 동일 도즈에서 더 많은 광자 흡수 → 확률론적 효과 감소

## 참고문헌
- Gallatin, G.M. et al., "Calibration of stochastic EUV resist model" (2012)
- Gao, P. et al., "Stochastic model for EUV resist" (2012)
- Inpria Corp. organometallic photoresist EUV papers

## 태그
`Model`, `SPIE-JMM`, `EUV`, `OrganometallicResist`, `StochasticModel`, `Calibration`, `LER`, `Aggregation`, `Inpria`, `2021`
