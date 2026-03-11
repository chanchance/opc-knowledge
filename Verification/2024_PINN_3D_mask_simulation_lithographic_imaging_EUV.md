# 3D Mask Simulation and Lithographic Imaging Using Physics-Informed Neural Networks

## 메타데이터
- **저자**: V. Medvedev, A. Erdmann, A. Rosskopf
- **연도**: 2024
- **게재지**: Proc. SPIE 12953, Optical and EUV Nanolithography XXXVII, 129530N (2024년 4월 10일)
- **DOI/URL**: https://doi.org/10.1117/12.3010466

## 핵심 요약
계산 리소그래피와 EUV 리소그래피 공정 설계 최적화에서는 마스크에서의 EUV 광 회절에 대한 엄밀한 모델링이 필요하다. 기존 전자기장(EMF) 솔버는 대규모 기술 문제에 비효율적이고, 순수 딥러닝은 대량의 고비용 시뮬레이션/측정 데이터가 필요하다. 이 논문은 물리 정보 신경망(PINN)을 EUV 마스크 회절 시뮬레이션에 적용하여 두 한계를 극복한다.

## 주요 기여
1. **MaxwellNet EUV 마스크 확장**: 기존 MaxwellNet을 반사형 EUV 마스크에서의 광 회절 시뮬레이션으로 확장
2. **PINN 기반 3D 마스크 시뮬레이션**: Maxwell 방정식을 물리 제약으로 통합하여 데이터 효율적인 3D 마스크 EMF 솔버 구현
3. **리소그래피 메트릭 예측**: 예측된 회절 스펙트럼과 이미지 시뮬레이션을 결합하여 NILS, DOF 등 핵심 리소그래피 지표 및 마스크 3D 효과 평가
4. **데이터 효율성**: 순수 데이터 기반 방법 대비 훨씬 적은 훈련 데이터로 고정밀 마스크 3D 효과 예측 가능

## 검증 방법론
- PINN 예측 회절 스펙트럼과 RCWA 등 rigorous EMF 솔버 결과 비교
- 이미지 시뮬레이션 연계 후 마스크 3D 효과(H/V 비대칭, 위상 오차 등) 예측 정확도 평가
- 다양한 EUV 마스크 패턴(L/S, contact)에서 PINN 일반화 성능 검증

## OPC 툴 구현 관련성
- EUV OPC 엔진의 마스크 3D 모델 컴포넌트를 PINN 기반으로 구현할 때 핵심 참고
- `skopc/modeling/` LithoEngine 내 EUV 마스크 시뮬레이션 가속화에 PINN 아키텍처 활용 가능
- 물리 기반 정규화로 학습 데이터 수요를 줄이는 전략을 GNN-OPC 모델 훈련에도 응용 가능
- 2025_hybrid_mask3D_modeling_physics_ML_EUV.md와 연계하여 M3D 모델링 전략 설계

## 태그
`Verification`, `SPIE`, `EUV`, `PINN`, `Physics_Informed`, `Mask3D`, `Electromagnetic`, `MaxwellNet`, `Simulation`, `2024`
