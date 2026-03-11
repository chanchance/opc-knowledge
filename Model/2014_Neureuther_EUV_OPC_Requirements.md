# EUV OPC Modeling and Correction Requirements

## 메타데이터
- **저자**: Neureuther, A. R. et al. (UC Berkeley / imec)
- **연도**: 2014
- **게재지**: Proc. SPIE 9048, Extreme Ultraviolet (EUV) Lithography V
- **DOI/URL**: https://doi.org/10.1117/12.2046341
- **인용수**: ~50

## 핵심 요약
EUV 리소그래피에서의 OPC 모델링 및 보정 요구사항을 10nm 노드를 예제로 종합적으로 분석한다. 웨이퍼 및 마스크 공정 데이터를 수집하여 캘리브레이션·검증 패턴에 적용하고, 마스크 제조 오차(MFE)와 OPC 모델 상호작용을 규명한다. 컴팩트 마스크 위상 모델(compact mask topography model)의 OPC 정확도 기여도를 엄밀 시뮬레이션과 비교 분석한다.

## 주요 기여
1. 10nm 노드 EUV OPC를 위한 모델 요구사항 최초 체계화
2. 마스크 제조 오차(MFE)/OPC 모델 상호작용 정량 분석
3. 컴팩트 M3D 모델 vs. 엄밀 EMF 시뮬레이션 정확도 비교
4. 대규모 데이터셋 기반 EUV OPC 모델 피팅 방법론
5. EUV 그림자 효과(shadowing), 플레어(flare) 보정 통합 모델 제시

## 모델 수식/아키텍처

**EUV 마스크 그림자 효과 (비텔레센트릭):**
```
Δx_shadow = H_mask · tan(θ_chief) / M
```
H_mask = 마스크 흡수체 높이, θ_chief = chief ray 각도, M = 축소비

**EUV 컴팩트 M3D 보정:**
```
TCC_eff(f,g; f',g') = TCC_Kirchhoff · (1 + δTCC_M3D(f,g,pitch))
```
δTCC_M3D = 마스크 두께 효과에 의한 TCC 섭동 항

**플레어 보정:**
```
I_flare(x,y) = I_ideal(x,y) + F · ∫∫ I_ideal(x',y') · PSF_flare(x-x', y-y') dx'dy'
```
F = flare level (~수%), PSF_flare = 광범위 점확산함수

**EUV OPC 모델 피팅 (대규모 데이터셋):**
```
min_{θ} Σ_i w_i · (CD_sim(θ, pattern_i) - CD_meas,i)²
subject to: ||θ|| ≤ θ_max (정규화)
```

**검증 메트릭:**
```
EPE_rms = sqrt(mean((predicted_edge - measured_edge)²))
EPE_3σ = 3 · std(EPE)
```

## 모델 유형
- [x] 광학 모델 (EUV 광학계, M3D)
- [x] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- EUV OPC 모델은 ArF 모델 대비 추가 고려사항:
  1. 그림자 효과 (chief ray angle ~6°)
  2. 마스크 흡수체 3D 효과 (EUV M3D)
  3. 플레어 (~5-10% 수준)
  4. 확률론적 레지스트 효과
- skopc/modeling/euv_model/ 구현 시 핵심 참조
- 컴팩트 M3D 모델: SOCS 커널에 방향 의존 보정 항 추가로 구현 가능

## 참고문헌
- Gallatin, G.M. et al., "Calibration of stochastic EUV resist model" (2012)
- Erdmann, A. et al., "Mask 3D effects on resist calibration" (2009)
- Mack, C.A., "Comprehensive EUV lithography model" (2011)

## 태그
`Model`, `SPIE`, `EUV`, `OPCModel`, `MaskTopography`, `Shadowing`, `Flare`, `Calibration`, `10nmNode`, `2014`
