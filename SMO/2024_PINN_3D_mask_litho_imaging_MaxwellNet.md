# 3D Mask Simulation and Lithographic Imaging Using Physics-Informed Neural Networks

## 메타데이터
- **저자**: (SPIE 12953 저자 정보)
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 129530N (2024)
- **DOI/URL**: https://doi.org/10.1117/12.3010466

## 핵심 요약
물리 정보 신경망(PINN)을 활용한 3D 마스크 시뮬레이션과 리소그래피 이미징 방법론을 제시한다. MaxwellNet을 EUV 반사형 마스크의 빛 회절 시뮬레이션에 적용하고, PINN의 리소그래피 지표 예측 성능과 M3D 효과 포착 능력을 평가한다.

## 주요 기여
1. **MaxwellNet EUV 마스크 적용**: MaxwellNet PINN 아키텍처를 EUV 반사형 마스크 시뮬레이션에 확장
2. **리소그래피 지표 예측**: PINN으로 NILS, 공정 창, CD 등 리소그래피 지표 직접 예측
3. **M3D 효과 포착**: EUV 마스크 3D 토포그래피 효과를 PINN으로 모델링
4. **PINN 성능 평가**: RCWA 대비 정확도와 속도 트레이드오프 정량화

## 알고리즘/수식
### MaxwellNet PINN 구조
```
Maxwell 방정식 기반 PINN:
  손실 함수:
    L = L_data + λ_pde · L_pde + λ_bc · L_bc

  L_pde: Maxwell 방정식 잔차
    ∇ × E = iωμH
    ∇ × H = -iωεE + J
    → 전자기장이 물리 법칙 만족하도록 강제

  MaxwellNet 입력:
    - 마스크 기하학 (패턴 형상)
    - EUV 조명 조건 (파장, 입사각)
    - 마스크 재료 광학 상수

  출력:
    - 회절 근장(near-field) 분포
    - 원장(far-field) 회절 스펙트럼
    - M3D 효과 포함 이미지 강도
```

### 리소그래피 지표 예측
```
리소그래피 지표 직접 예측:
  NILS = d(ln I)/dx × CD / 2  (정규화 이미지 로그 기울기)
  PW = {(dose, focus) : CD ∈ [target ± tolerance]}
  CD = f(aerial_image, resist_model)

PINN 대 RCWA 비교:
  정확도: |T_PINN - T_RCWA| < ε (수% 오차)
  속도: RCWA 분~시간 → PINN 밀리초
  가속: 100x ~ 1000x

물리 제약 이점:
  외삽 성능: 훈련 범위 밖 패턴에도 일반화
  데이터 효율: 수백 RCWA 데이터로 충분
```

## OPC 툴 SMO 구현 관련성
- MaxwellNet M3D 모델: SKOPC SMO/OPC 엔진에서 MaxwellNet 기반 M3D 대리 모델 채택
- 리소그래피 지표 직접 예측: NILS/PW를 PINN으로 빠르게 평가하여 SMO 가속화
- M3D 포함 OPC: PINN M3D 모델을 OPC 보정 루프에 통합
- 물리 제약 ML: 데이터 효율적이고 물리적으로 타당한 ML 기반 OPC/SMO 모델 설계

## 태그
`PINN`, `MaxwellNet`, `M3D`, `EUV`, `lithography_simulation`, `neural_network`, `NILS`, `process_window`, `OPC`, `SMO`, `SPIE`, `2024`
