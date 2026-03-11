# 3D Mask Simulation and Lithographic Imaging Using Physics-Informed Neural Networks

## 메타데이터
- **저자**: V. Medvedev, A. Erdmann, A. Rosskopf
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 129530N
- **DOI/URL**: https://doi.org/10.1117/12.3010466

## 핵심 요약
물리 정보 기반 신경망(PINN)을 EUV 마스크 3D 시뮬레이션에 적용한다. MaxwellNet 모델을 반사형 EUV 마스크의 광 회절 시뮬레이션으로 확장하여, 대용량 학습 데이터 없이도 M3D 효과를 예측하고 리소그래픽 메트릭을 평가한다.

## 주요 기여
1. MaxwellNet PINN을 반사형 EUV 마스크 회절 시뮬레이션으로 확장
2. 대용량 학습 데이터 없이도 물리 법칙으로 학습하는 PINN의 데이터 효율성 입증
3. EUV M3D 효과 예측 및 리소그래픽 메트릭 평가 파이프라인 구축
4. 전통적 EM 솔버(FDTD/RCWA) 및 순수 DNN의 한계를 동시에 극복
5. Erdmann 그룹(프라운호퍼)의 PINN 기반 EUV M3D 시뮬레이션 연구

## 모델 수식/아키텍처
- **MaxwellNet PINN**:
  - 물리 제약: ∇×∇×E - k²ε(x)E = 0 (맥스웰 방정식)
  - 신경망: 공간 좌표 (x,y,z) → 전기장 (E_x, E_y, E_z)
  - 손실 = 물리 잔차 손실 + 경계 조건 손실 (데이터 손실 불필요)
- EUV 반사형 마스크 적용:
  - Mo/Si 다층 반사막 + Ta 흡수재 스택 모델링
  - 6° 경사 입사 EUV 조명 조건
- 리소그래픽 메트릭: CD, 공정 윈도우, 이미지 로그 기울기(ILS)

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [x] ML/DL
- [x] 하이브리드 (물리 법칙 내장 PINN)

## OPC 툴 구현 관련성
- SKOPC EUV M3D 계산에서 FDTD/RCWA를 PINN으로 가속하는 방향 제시
- 데이터 효율적 M3D 모델: 학습 데이터 부족 환경에서 PINN 적용 가능
- `2024_Ju_PINN_Mask3D_Lithography.md`와 함께 PINN 기반 M3D 연구 계열
- Erdmann(2009/2019/2021) 그룹의 M3D 연구 최신 딥러닝 확장

## 태그
`Model`, `PINN`, `M3D`, `EUV`, `MaxwellNet`, `PhysicsInformed`, `NeuralNetwork`, `Erdmann`, `SPIE`
