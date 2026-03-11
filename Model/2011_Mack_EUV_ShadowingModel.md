# Shadowing Effect Modeling and Compensation for EUV Lithography

## 메타데이터
- **저자**: Mack, C. A. et al. (Lithoguru / imec)
- **연도**: 2011
- **게재지**: Proc. SPIE 7969, Optical Microlithography XXIV
- **DOI/URL**: https://doi.org/10.1117/12.881713
- **인용수**: ~65

## 핵심 요약
EUV 리소그래피의 반사 광학계에서 비텔레센트릭(non-telecentric) 조명에 의한 마스크 그림자 효과(shadowing effect)를 모델링하고 이를 OPC로 보정하는 방법을 제시한다. 그림자 효과는 피처 방향과 슬릿 위치에 따라 수 nm의 CD 오차를 유발하며, 이를 OPC 모델에 통합하여 보정하지 않으면 EUV 패터닝 정확도가 크게 저하됨을 실험으로 확인한다.

## 주요 기여
1. EUV 마스크 그림자 효과의 방향·슬릿 의존적 CD 오차 정량화 (최대 수 nm)
2. Chief Ray Angle(CRA)과 마스크 흡수체 두께에 의한 그림자 모델 수립
3. 그림자 보정을 OPC 모델에 통합하는 방법론
4. 슬릿 위치(cross-slit) 의존 CD 변동의 OPC 모델 캘리브레이션 전략
5. 그림자 보정 전/후 패터닝 정확도 비교 (CD 오차 80% 감소)

## 모델 수식/아키텍처

**EUV 마스크 그림자 기하학:**
```
Δx_shadow = H_absorber · tan(θ_CRA) / M
```
H_absorber = 마스크 흡수체 높이 (~56-84nm TaN)
θ_CRA = chief ray 입사각 (~6° for 0.33NA ASML NXE)
M = 축소비 (4×)

**방향 의존 그림자 효과:**
```
H_features (horizontal): ΔCD_H = 2 · Δx_shadow  [양쪽 엣지 모두 이동]
V_features (vertical): ΔCD_V = 0  [엣지 이동 없음, 단 위치 이동]
Diagonal: ΔCD_diag = Δx_shadow · cos(θ_feature)
```

**슬릿 위치 의존 best focus shift:**
```
ΔBF_shadow(y_slit) = -H_absorber · (NA/M) · sin(θ_CRA(y_slit)) / λ
```
y_slit = 슬릿 상의 위치 (슬릿 중심 = 0)

**OPC 보정 (그림자 보정 항):**
```
CD_corrected(x,y) = CD_target + ΔCD_shadow(orientation, y_slit)
mask_CD = CD_corrected × M + OPC_corrections
```

**그림자 보정 OPC 모델 통합:**
```
TCC_eff(f, y_slit) = TCC_nominal(f) · Phase_shadow(f, y_slit)
Phase_shadow = exp[-i·2π·f·Δx_shadow(y_slit)]
```

## 모델 유형
- [x] 광학 모델 (EUV 그림자 효과)
- [ ] 레지스트 모델
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- EUV OPC 필수 보정 항: 플레어 + 그림자 + 근접 효과
- skopc/modeling/euv_shadow.py: Chief Ray Angle 기반 그림자 모델 구현
- 슬릿 위치별 OPC 모델 분기 (across-slit variation model)
- 마스크 흡수체 재질/두께 변경 시 그림자 효과 재캘리브레이션 필요
- 고NA EUV (0.55NA, anamorphic optics): 그림자 효과 더욱 복잡해짐

## 참고문헌
- Flagello, D.G. et al., "EUV flare and proximity modeling" (2011)
- Neureuther, A.R. et al., "EUV OPC modeling requirements" (2014)
- ASML NXE:3300/3400 scanner specifications

## 태그
`Model`, `SPIE`, `EUV`, `Shadowing`, `NonTelecentric`, `ChiefRayAngle`, `OPC`, `CrossSlit`, `Calibration`, `2011`
