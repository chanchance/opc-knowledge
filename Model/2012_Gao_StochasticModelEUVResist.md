# Calibration and Verification of a Stochastic Model for EUV Resist

## 메타데이터
- **저자**: Gao (IMEC 연구팀)
- **연도**: 2012
- **게재지/학회**: SPIE Advanced Lithography, Proc. SPIE 8322 (Optical Microlithography XXV)
- **DOI/URL**: https://doi.org/10.1117/12.917804
- **인용수**: 80+

## 핵심 요약
EUV 리소그래피용 레지스트의 확률론적(stochastic) 모델을 구축하고 보정(calibration)하는 방법론을 제시한 선구적 논문. EUV 리소그래피에서는 광자 수가 매우 적어 포아송 분포(Poisson distribution)를 따르는 광자 산탄 잡음(photon shot noise)이 선 엣지 거칠기(LER: Line Edge Roughness)의 주요 원인이 된다. imec 기준 EUV 레지스트(Shinetsu SEVR140)에 대해 250개 이상의 CD 및 LER 측정 데이터로 모델을 보정하고, 1D/2D 패턴으로 검증한다. 이 확률론적 모델은 EUV OPC에서 LER, 결함률, 공정 윈도우 예측에 필수적이다.

## 주요 기여
- EUV 레지스트용 확률론적 모델 보정 및 검증 방법론 확립
- 250개 이상 CD 및 LER 측정 데이터 기반 체계적 보정
- 광자 산탄 잡음이 LER의 ~60%를 기여함을 정량적으로 입증
- 1D/2D 패턴에서의 확률론적 결함 예측 모델 검증
- Ideal Resist Model(IRM)을 이용한 PSN 기여분 분리 방법 제안

## 모델 아키텍처/수식
**EUV 리소그래피의 확률론적 이미지 형성:**

평균 광자 수:
```
<n_ph>(x, y) = E₀ · σ_abs · I(x, y) / (hν)
```
- E₀: 노광 에너지 (dose, mJ/cm²)
- σ_abs: EUV 흡수 단면적 (ArF 대비 ~4× 높음)
- I(x, y): 정규화된 이미지 강도
- hν: EUV 광자 에너지 (13.5nm → 91.8eV)

**광자 산탄 잡음 (Photon Shot Noise):**
광자 수는 포아송 분포를 따름:
```
P(n_ph) = <n_ph>^n · exp(-<n_ph>) / n!
σ_PSN = √<n_ph>    (표준편차)
```

**화학 증폭 레지스트(CAR) 확률론적 반응:**
```
산 생성: n_acid ~ Poisson(<n_ph> · QY · n_mol)
확산: r_diffusion ~ Normal(0, σ_peb²)
중화: n_acid_remaining ~ Binomial(n_acid, 1-P_quench)
```
- QY: 양자 수율(quantum yield)
- n_mol: 단위 부피당 분자 수

**레지스트 현상 확률론적 모델:**
임계 농도 T에서의 현상 확률:
```
P_develop(x) = P(A_peb(x) ≥ T)
```
LER 예측:
```
LER² = LER_PSN² + LER_chem²
LER_PSN ≈ σ_PSN / (dI/dx)|_{edge}
```

**Ideal Resist Model (IRM):**
순수 PSN 기여분 분리:
```
LER_IRM = LER_measured - LER_chemical
         ≈ 0.6 × LER_total
```

**보정 파라미터 세트:**
- {σ_abs, QY, σ_peb, T, σ_quench, n_mol}
- 보정 데이터: imec Shinetsu SEVR140, EUV 13.5nm
- 측정 데이터: >250 CD values + LER measurements

**보정 결과 (imec SEVR140):**
- EUV 감도: 1.4~20 mJ/cm² (다양한 조성)
- LER: 3~5nm 범위
- PSN 기여: ~60% of total LER

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [ ] ML/DL 모델
- [ ] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 EUV 공정 시나리오(`recipes/example_euv.yaml`)에서 레지스트 모델 보정 시 핵심 참조. TorchResist의 확률론적 확장에 이 모델의 수식 활용 가능. EUV LWR/LER 예측 기능을 SKOPC에 추가할 때 PSN 기여분 계산 수식 직접 구현 가능. 특히 EUV 공정 윈도우(PWO)에서 확률론적 결함률을 포함하는 것이 중요하며, 이 논문의 P_develop(x) 모델이 기반이 됨.

## 참고문헌 (핵심)
- Brainard, R. et al., "Shot noise, LER, and quantum efficiency of EUV photoresists," SPIE 5374 (2004)
- Mack, C.A., "Stochastic model for photoresist dissolution," J. Electrochem. Soc. (1992)
- Flanagin, L.W. et al., "Surface roughness evolution during photoresist dissolution," J. Vac. Sci. Technol. B (1999)
- Kozawa, T. et al., "Stochastic simulation of chemically amplified resists," Jpn. J. Appl. Phys. (2007)

## 태그
`Model`, `OPC`, `EUV`, `ResistModel`, `Stochastic`, `LER`, `ShotNoise`, `PSN`, `Calibration`, `SPIE`, `LWR`, `OrganometallicResist`, `DefectPrediction`
