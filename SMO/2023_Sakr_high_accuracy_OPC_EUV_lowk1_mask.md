# High Accuracy OPC Modeling for New EUV Low-K1 Mask Technology Options

## 메타데이터
- **저자**: Enas Sakr, Rob DeLancey, Wolfgang Hoppe, Zac Levinson, Robert Iwanow, Ryan Chen, Delian Yang, Kevin Lucas
- **연도**: 2023
- **게재지**: Proc. SPIE 12495, DTCO and Computational Patterning II, 124950P (28 April 2023)
- **DOI/URL**: https://doi.org/10.1117/12.2658720

## 핵심 요약
EUV 리소그래피의 프로세스 기술 및 레이아웃 설계 개선으로 발전해온 EUV 리소그래피에서, 설계-리소그래피 상호작용을 이해하기 위한 정확한 예측 능력의 중요성을 강조한다. EUV 특이 물리 현상(그림자 효과, 플레어, 마스크 토포그래피 효과)을 포함한 새로운 EUV 저-k1 마스크 기술 옵션(low-n/low-k 흡수층, attPSM)에 대한 고정밀 OPC 모델링 방법론을 제시한다.

## 주요 기여
1. **EUV 저-k1 마스크 OPC 모델링**: low-n/low-k 흡수층 및 attPSM 마스크 옵션에 대한 고정밀 OPC 모델 개발
2. **EUV 특이 효과 모델링**: 그림자 효과(shadowing), 플레어(flare), 마스크 토포그래피(mask topography) 효과의 정밀 모델링
3. **예측 정확도 향상**: 설계-리소그래피 상호작용 이해를 위한 정확한 예측 능력 제공
4. **새 마스크 기술 옵션 지원**: 차세대 EUV OPC 플로우에서 대안 흡수층 마스크 지원

## 알고리즘/수식
### EUV 저-k1 OPC 모델 구성요소
```
EUV OPC 모델 = 광학 모델 + 레지스트 모델 + EUV 특이 효과

1. 광학 모델 (Hopkins/Abbe):
   I(x) = Σ_{m,n} J(f_m) · |Σ_k T(f_m, f_k) · M(f_k)|²
   여기서 T: EUV 마스크 회절 전달 함수

2. EUV 특이 효과:
   - 그림자 효과: I_shadow(x) = I(x) · F_shadow(x, t_abs)
   - 플레어: I_flare(x) = I(x) + I_flare_bg
   - 마스크 토포그래피 (M3D): RCWA 기반 엄격 계산

3. 새 마스크 흡수층 모델:
   - low-n/low-k 흡수층: (n, k) = (n_low, k_low) at 13.5nm
   - attPSM: 부분 반사 + 위상 이동 = (R_att, φ_shift)
   - 각 재료에 대한 T(f) 재계산
```

### OPC 모델 보정 방법
```
모델 보정:
  min_{model_params} Σ_CD ||CD_sim - CD_meas||²

EUV 특이 보정 파라미터:
  - 그림자 보정 계수: α_shadow
  - 플레어 반경 및 크기: (r_flare, A_flare)
  - M3D 보정 Look-Up Table
```

## OPC 툴 SMO 구현 관련성
- EUV OPC 모델 정밀도가 SMO 성능에 직접 영향
- low-n/attPSM 마스크 지원 시 OPC 모델 재보정 필요
- EUV 특이 효과(그림자, 플레어, M3D)를 SMO 비용 함수 계산에 통합
- SKOPC OPC 모델 모듈에서 EUV 마스크 타입별 모델 분기 설계 참조

## 태그
`OPC`, `EUV`, `low_k1`, `mask_absorber`, `low_n`, `attPSM`, `shadowing`, `flare`, `M3D`, `model_calibration`, `DTCO`, `SPIE`
