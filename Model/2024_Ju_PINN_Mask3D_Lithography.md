# 3D Mask Simulation and Lithographic Imaging Using Physics-Informed Neural Networks

## 메타데이터
- **저자**: Ju, X. et al. (KLA / UC Berkeley)
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII
- **DOI/URL**: https://doi.org/10.1117/12.3010466
- **인용수**: ~12

## 핵심 요약
EUV 리소그래피의 복잡한 광학 문제를 해결하기 위해 물리 정보 신경망(PINN: Physics-Informed Neural Networks)을 3D 마스크 시뮬레이션과 리소그래피 이미징에 적용한다. Maxwell 방정식을 기반으로 학습된 MaxwellNet을 반사형 EUV 마스크의 광 회절 시뮬레이션으로 확장하고, 예측된 회절 스펙트럼을 이미지 시뮬레이션에 결합하여 리소그래피 메트릭과 마스크 3D 효과 예측 성능을 평가한다.

## 주요 기여
1. MaxwellNet(PINN 기반)을 EUV 반사형 마스크 3D 시뮬레이션으로 최초 확장
2. Maxwell 방정식을 손실 함수에 물리 제약으로 내장 → 학습 데이터 효율 향상
3. RCWA 대비 수십 배 빠른 EUV 마스크 회절 스펙트럼 예측
4. PINN 회절 스펙트럼 → 공중상 이미징 파이프라인 연동 검증
5. 마스크 3D 효과(BFS, MEEF 변동) 예측 정확도 RCWA와 비교 분석

## 모델 수식/아키텍처

**Maxwell 방정식 (PINN 물리 제약):**
```
∇ × E = iωμH
∇ × H = -iωεE
```
→ 손실 함수에 PDE 잔차 항으로 추가:
```
L_physics = ||∇×E - iωμH||² + ||∇×H + iωεE||²
```

**PINN 전체 손실:**
```
L_total = L_data + λ_phys · L_physics + λ_bc · L_boundary
```
L_data = 레이블된 RCWA 데이터와의 오차
L_boundary = 경계 조건 잔차

**MaxwellNet 아키텍처:**
```
Input: mask_geometry (흡수체 형상, 두께, 재질)
       illumination (파장, 입사각, 편광)
Hidden: 5-8 fully-connected layers (256-512 units), GELU activation
Output: E_scattered(x,y,z) 또는 near-field amplitude
```

**회절 스펙트럼 → 공중상 연동:**
```
E_diff(f) = FFT[E_scattered(x,y)]   [근접장 → 원접장 변환]
I(x,y) = Σ_k λ_k|∫ φ_k(f)·E_diff(f)·e^{i2πfx}df|²
```

**PINN 예측 정확도:**
```
Error_field = ||E_PINN - E_RCWA||_2 / ||E_RCWA||_2 × 100%
목표: < 2% (EUV 마스크 표준 구조)
```

## 모델 유형
- [x] 광학 모델 (M3D EMF + PINN)
- [ ] 레지스트 모델
- [x] ML/DL (Physics-Informed Neural Network)
- [x] 하이브리드 (물리 방정식 내장 신경망)

## OPC 툴 구현 관련성
- 기존 RCWA 대체 고속 M3D 시뮬레이터로 활용 가능
- skopc M3D 모듈에 PINN 옵션 추가 → 학습 후 초고속 마스크 3D 예측
- 학습 데이터: RCWA 계산 결과 (다양한 피치/두께/재질 조합)
- EUV 고NA(0.55NA) 전환 시 계산 복잡도 증가 → PINN 가속 효과 극대화
- 한계: 학습 분포 밖 구조(novel mask geometry)에 대한 외삽 불확실성

## 참고문헌
- Raissi, M. et al., "Physics-informed neural networks" (2019, JCP)
- Tyminski, J.K. et al., "Fast and accurate 3D mask model" (2007)
- Lam, M. et al., "M3D-EMF OPC prediction improvements" (2012)

## 태그
`Model`, `SPIE`, `PINN`, `PhysicsInformed`, `NeuralNetwork`, `Mask3D`, `EUV`, `MaxwellNet`, `HybridModel`, `2024`
