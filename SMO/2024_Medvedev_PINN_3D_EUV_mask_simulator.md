# 3D EUV Mask Simulator Based on Physics-Informed Neural Networks: Effects of Polarization and Illumination

## 메타데이터
- **저자**: V. Medvedev, A. Erdmann, A. Rosskopf
- **연도**: 2024
- **게재지**: Proc. SPIE 13023, Computational Optics 2024, 1302304 (17 June 2024)
- **DOI/URL**: https://doi.org/10.1117/12.3013159

## 핵심 요약
물리 정보 신경망(PINN, Physics-Informed Neural Networks)을 기반으로 한 3D EUV 마스크 시뮬레이터를 개발하여 편광 효과와 조명 설정의 영향을 연구한다. 기존 전자기장 솔버의 비효율성과 딥러닝의 대규모 데이터 의존성 문제를 PINN으로 극복하며, 이전 PINN 연구를 편광 효과와 가변 조명 설정으로 확장한다.

## 주요 기여
1. **PINN 기반 3D EUV 마스크 시뮬레이터**: Maxwell 방정식을 손실 함수에 통합한 PINN
2. **편광 효과 포함**: EUV 조명의 편광 상태가 마스크 회절에 미치는 영향 모델링
3. **가변 조명 지원**: 다양한 조명 설정(σ, 방향, 편광)에 대한 일반화된 시뮬레이션
4. **데이터 효율성**: 소량의 EM 시뮬레이션 데이터로 물리 제약 기반 학습

## 알고리즘/수식
### PINN 기반 EUV 마스크 시뮬레이터
```
물리 정보 신경망 (PINN):
  손실 함수:
    L = L_data + λ_physics · L_physics

  L_physics: Maxwell 방정식 잔차
    L_physics = ||∇×E - ∂B/∂t||² + ||∇×H - J - ∂D/∂t||²
    → 전자기장 해가 물리 법칙을 만족하도록 강제

  L_data: 훈련 데이터(RCWA 결과)와의 불일치
    L_data = ||E_PINN - E_RCWA||²

편광 효과 모델링:
  입력: 마스크 레이아웃 M + 편광 상태 p (TE/TM/circular)
  출력: 편광별 회절 스펙트럼 T_M3D(fx, fy, p)

가변 조명:
  입력 확장: M + p + σ + θ_incident
  → 다양한 조명 조건에 대한 일반화
```

### PINN vs RCWA 성능
```
정확도:
  |T_PINN - T_RCWA| < ε (ε: 허용 오차 기준)
  물리 제약으로 과적합 방지 → 외삽 성능 향상

속도:
  RCWA: 분~시간 단위 (패턴 복잡도 의존)
  PINN 추론: 밀리초 단위
  가속 배율: 100x ~ 10000x

데이터 효율성:
  기존 순수 데이터 NN: 수천~수만 RCWA 데이터 필요
  PINN: 수백 데이터로 충분 (물리 제약으로 보완)
```

## OPC 툴 SMO 구현 관련성
- PINN 기반 M3D 모델: SKOPC OPC/SMO 엔진에서 PINN M3D 대리 모델 채택
- 편광 인식 M3D: 편광 최적화(SMPO)와 M3D 계산 통합 가능
- 가변 조명 지원: SMO에서 다양한 소스 형상에 대한 M3D 예측 일반화
- 물리 제약 ML: 데이터 효율적이고 물리적으로 타당한 ML 모델 설계 방향

## 태그
`PINN`, `physics_informed`, `neural_network`, `M3D`, `EUV`, `polarization`, `illumination`, `EMF`, `RCWA`, `deep_learning`, `SPIE`, `2024`
