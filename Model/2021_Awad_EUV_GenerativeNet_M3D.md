# Accurate Prediction of EUV Lithographic Images and 3D Mask Effects Using Generative Networks

## 메타데이터
- **저자**: Abdalaziz Awad, Philipp Brendel, Peter Evanschitzky, Dereje S. Woldeamanual, Andreas Rosskopf, Andreas Erdmann
- **연도**: 2021
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology, Vol. 20, No. 4, 043201
- **DOI/URL**: https://doi.org/10.1117/1.JMM.20.4.043201

## 핵심 요약
딥러닝 생성 네트워크(generative network)를 활용하여 EUV 리소그래피 이미지와 3D 마스크 효과(M3D)를 정확하게 예측한다. EMF 시뮬레이션의 계산 병목을 딥러닝으로 극복하면서 EUV 공정 변동성까지 반영한다.

## 주요 기여
1. 생성 네트워크(GAN 또는 변분 오토인코더 계열)로 EUV 공중 이미지 정확 예측
2. M3D 효과를 딥러닝으로 모델링하여 엄밀한 EMF 시뮬레이션 대체
3. EUV 공정 변동성(초점, 노광량 변화) 반영한 이미지 예측
4. 계산 속도: 엄밀 EMF 시뮬레이션 대비 수십~수백 배 가속
5. Erdmann 그룹(프라운호퍼)의 EUV M3D 딥러닝 시뮬레이션 연구

## 모델 수식/아키텍처
- **생성 네트워크**: mask_layout + process_conditions → EUV_aerial_image
- 조건부 생성 구조: 초점(F), 노광량(D), NA 등을 조건으로 입력
- M3D 효과 인코딩: 마스크 두께, 흡수재 재료, 스택 구조를 특징으로 입력
- 손실 함수: L1/L2 픽셀 손실 + 지각 손실(perceptual loss) + GAN 손실
- 검증: FDTD/RCWA 기반 엄밀 시뮬레이션과 비교

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [x] ML/DL
- [x] 하이브리드

## OPC 툴 구현 관련성
- SKOPC EUV 광학 시뮬레이션 모듈의 M3D 효과 가속에 생성 네트워크 적용 가능
- Erdmann(2009/2019) 그룹의 EUV M3D 연구 연속선상 딥러닝 확장
- `2024_Tanabe_CNN_EUV_M3D_Pretrain.md`와 함께 M3D 딥러닝 시뮬레이션 주요 사례
- EUV 공정 변동 시뮬레이션에서 몬테카를로 대체 가능성 제시

## 태그
`Model`, `EUV`, `M3D`, `GAN`, `GenerativeNetwork`, `DeepLearning`, `AerialImage`, `Erdmann`, `JMM`, `SPIE`
