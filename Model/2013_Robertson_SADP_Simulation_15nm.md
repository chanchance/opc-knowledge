# Simulation of Spacer-Based SADP (Self-Aligned Double-Patterning) for 15nm Half Pitch

## 메타데이터
- **저자**: Robertson, S. et al. (KLA-Tencor)
- **연도**: 2013
- **게재지**: Proc. SPIE 8683, Optical Microlithography XXVI
- **DOI/URL**: https://doi.org/10.1117/12.2013877
- **인용수**: ~45

## 핵심 요약
EUV 단일 노광으로 제작된 맨드릴(mandrel)을 기반으로 하는 스페이서(spacer) 방식 SADP(Self-Aligned Double Patterning) 공정을 15nm half pitch에서 PROLITH X4.2로 시뮬레이션한다. 리소그래피 맨드릴 단계, 스페이서 증착/에칭, 맨드릴 제거 각 단계를 순차적으로 모델링하여 최종 스페이서 패턴 형상을 예측하고, 실험 결과와 비교하여 시뮬레이션 정확도를 검증한다.

## 주요 기여
1. SADP 전체 공정(맨드릴 리소 → 스페이서 증착/에칭 → 맨드릴 제거)의 통합 시뮬레이션 방법론
2. PROLITH 기반 3D 레지스트 프로파일 + 스페이서 형상 연계 모델
3. 15nm half pitch EUV SADP 공정에서 시뮬레이션-실험 일치성 검증
4. 스페이서 CD 및 LWR에 대한 맨드릴 리소 조건(dose/focus) 민감도 분석
5. 컴팩트 바이어스(compact bias) 모델로 최종 OPC 형상 예측

## 모델 수식/아키텍처

**SADP 공정 순서 모델:**
```
Step 1: Mandrel lithography
  CD_mandrel = Litho_Model(mask_OPC, optical, resist, focus, dose)

Step 2: Spacer deposition (conformal ALD)
  t_spacer = target thickness (e.g. 7nm for 15nm HP)
  Spacer_profile = CD_mandrel + 2·t_spacer  (top) → tapered bottom

Step 3: Spacer etch (anisotropic RIE)
  CD_spacer_final = t_spacer ± δ_etch  (etch uniformity variation)

Step 4: Mandrel removal
  Final_CD = f(CD_spacer_final, etch_selectivity)
```

**스페이서 CD 예측 모델:**
```
CD_spacer = 2·t_ALD + CD_mandrel·f(mandrel_profile_angle)
          ≈ 2·t_ALD  (이상적 수직 맨드릴 프로파일 시)
```

**SADP 최종 피치 배가:**
```
HP_final = HP_mandrel / 2
HP_mandrel = 30nm (EUV) → HP_final = 15nm
```

**맨드릴 리소 민감도 분석:**
```
∂CD_spacer/∂dose = (∂CD_mandrel/∂dose) · (∂CD_spacer/∂CD_mandrel)
∂CD_spacer/∂focus = (∂CD_mandrel/∂focus) · (∂CD_spacer/∂CD_mandrel)
```

**LWR 전파:**
```
LWR_spacer² ≈ LWR_mandrel² + LWR_ALD² + LWR_etch²
```

## 모델 유형
- [x] 광학 모델 (EUV 맨드릴 리소 시뮬레이션)
- [x] 레지스트 모델 (3D 레지스트 프로파일)
- [ ] ML/DL
- [x] 하이브리드 (리소 + 증착/에칭 통합 공정 모델)

## OPC 툴 구현 관련성
- SADP OPC 구현: 맨드릴 마스크 OPC → 스페이서 CD 예측 → 최종 패턴 검증
- skopc SADP 모듈: PROLITH SADP 시뮬레이션 파이프라인 참조
- 맨드릴 리소 OPC가 최종 스페이서 CD를 결정 → 맨드릴 OPC 정밀도 중요
- 스페이서 두께 균일도(ALD uniformity)가 CD 균일도에 직접 영향
- 7/5nm 노드: SAQP(Self-Aligned Quadruple Patterning)로 확장

## 참고문헌
- Smayling, M.C. et al., "Double patterning from design to verification" (2012)
- Sturtevant, J. et al., "Roadmap to sub-nanometer OPC" (2012)
- KLA-Tencor PROLITH documentation

## 태그
`Model`, `SPIE`, `SADP`, `DoublePatterning`, `Spacer`, `Mandrel`, `EUV`, `15nm`, `ProcessSimulation`, `2013`
