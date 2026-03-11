# 3D NTD Resist Deformation Compact Model for OPC and ILT Applications

## 메타데이터
- **저자**: Latinwo, F. et al. (Synopsys)
- **연도**: 2018
- **게재지**: Proc. SPIE 10810, Optical/EUV Nanolithography XXXI
- **DOI/URL**: https://doi.org/10.1117/12.2501992
- **인용수**: ~28

## 핵심 요약
NTD(Negative-Tone Development) 레지스트의 PEB 단계 및 현상 공정에서 발생하는 광레지스트 수축(shrinkage) 효과를 3D OPC/ILT 응용을 위한 컴팩트 모델로 구현한다. NTD 레지스트의 독특한 변형(deformation) 거동을 캡처하여 OPC 및 ILT 플로우에서의 CD 예측 정확도를 향상시킨다.

## 주요 기여
1. NTD 레지스트 PEB + 현상 단계 수축/변형의 3D 컴팩트 모델 개발
2. PTD(Positive-Tone Development) 대비 NTD 특유의 변형 패턴 분석
3. 기본 수축·변형 거동을 리고러스 시뮬레이터와 컴팩트 모델 모두로 포착
4. OPC 및 ILT 플로우에 통합 가능한 효율적 컴팩트 모델 구현
5. NTD 레지스트 사용 레이어(Via, Contact)에서 모델 정확도 향상 실증

## 모델 수식/아키텍처

**NTD 레지스트 수축 메커니즘:**
```
PTD: 노광된 영역이 현상 → 수축 최소
NTD: 미노광 영역이 현상 → 잔류 레지스트가 노광 응력 받음
→ CD_NTD_printed = CD_mask - 2·δ_shrink_NTD
```

**3D 수축 변형 모델:**
```
u(x,y,z) = displacement field
σ(x,y,z) = stress = C : ε(u)
f_shrink(x,y,z) = PEB/development에서의 체적 수축력
```

**컴팩트 NTD 변형 모델:**
```
δ_NTD(edge) = f(CD, pitch, resist_height, exposure_dose)
            = α·CD + β/pitch + γ·H_resist + δ·log(dose) + ...
```
α, β, γ, δ = 캘리브레이션 계수

**OPC 타겟 보정:**
```
CD_mask_target = CD_wafer_target + 2·δ_NTD(CD_wafer_target, pitch, ...)
```

**ILT 비용함수 통합:**
```
Cost_ILT = ||I(mask) - I_target||² + λ_NTD·||δ_NTD(mask)||²
```

## 모델 유형
- [ ] 광학 모델
- [x] 레지스트 모델 (NTD 변형 컴팩트 모델)
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- EUV Via/Contact 레이어에서 NTD 레지스트 사용 증가 → NTD 모델 필수
- skopc/modeling/ntd_resist.py: 수축 변형 컴팩트 모델 구현
- OPC 타겟 설정: CD_wafer_target + NTD 수축 보정량 → 최종 마스크 CD
- ILT 플로우: NTD 변형 항을 ILT 비용함수에 추가하여 최적화
- Synopsys Proteus NTD 모델의 이론적 기반

## 참고문헌
- Chou, A. et al., "Resist shrinkage: rigorous simulations and compact model" (2020)
- Latinwo, F. et al., "Improving OPC modeling with resist deformation" (2023)
- Adam, K. et al., "Calibration of physical resist models" (2009)

## 태그
`Model`, `SPIE`, `NTD`, `ResistDeformation`, `Shrinkage`, `CompactModel`, `OPC`, `ILT`, `3D`, `2018`
