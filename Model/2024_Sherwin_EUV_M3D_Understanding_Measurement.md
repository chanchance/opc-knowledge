# Understanding and Measuring EUV Mask 3D Effects

## 메타데이터
- **저자**: Stuart Sherwin, Matt Hettermann, Dave Houser, Patrick Naulleau
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 129530F
- **DOI/URL**: https://doi.org/10.1117/12.3012400

## 핵심 요약
EUV 리소그래피에서 마스크 3D 효과(M3D)의 물리적 원인을 분석하고 실험적으로 측정하는 방법론을 제시한다. 위상 시프트 대 피치 의존성이 설정하는 aPSM 목표 위상 이동(~1.2π)을 포함한 M3D 효과의 근본 원인을 체계적으로 규명한다.

## 주요 기여
1. EUV 마스크 3D 효과의 물리적 원인 체계적 분석
2. 위상 시프트-피치 의존성: aPSM 최적 위상 이동이 π가 아닌 ~1.2π임을 규명
3. M3D 효과의 실험적 측정 방법론 개발 (AIMS 또는 웨이퍼 레벨)
4. M3D 효과가 OPC 모델 정확도에 미치는 영향 정량화
5. 마스크 흡수재 구조(Ta, Mo/Si 다층막 등)에 따른 M3D 변화 분석

## 모델 수식/아키텍처
- **M3D 위상 오차**: Δφ = φ_3D_simulation - φ_thin_mask_approx
- **위상-피치 의존성**: φ_optimal = f(pitch, NA, λ, mask_stack_geometry)
- aPSM 최적 위상 이동: φ_target ≈ 1.2π (thin-mask 근사의 π와 차이)
- 측정 방법: 다양한 피치와 패턴 크기에서 공중 이미지 및 웨이퍼 CD 측정
- M3D 보정: OPC 모델에서 위상 오차를 보정 커널로 통합

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [ ] ML/DL
- [ ] 하이브리드

## OPC 툴 구현 관련성
- SKOPC EUV 광학 모델에서 M3D 위상 오차 보정 기능 구현 시 핵심 참조
- aPSM(attenuated PSM) 마스크 타입 지원 시 최적 위상 이동 설정 기준
- EUV OPC 모델 교정에서 M3D 효과를 별도 측정·보정하는 흐름 구축
- `2025_Chen_HybridM3D_ML_Physical.md`, `2024_Tanabe_CNN_EUV_M3D_Pretrain.md` 등과 연계

## 태그
`Model`, `EUV`, `M3D`, `MaskEffect`, `aPSM`, `PhaseShift`, `Measurement`, `OPC`, `SPIE`
