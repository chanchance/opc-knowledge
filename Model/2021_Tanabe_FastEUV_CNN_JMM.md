# Fast EUV Lithography Simulation Using Convolutional Neural Network

## 메타데이터
- **저자**: Hiroyoshi Tanabe, Shimpei Sato, Atsushi Takahashi
- **연도**: 2021
- **게재지**: Journal of Micro/Nanopatterning, Materials, and Metrology, Vol. 20, No. 4, 041202
- **DOI/URL**: https://doi.org/10.1117/1.JMM.20.4.041202

## 핵심 요약
2D EUV 마스크 패턴에서 회절 진폭(diffraction amplitude)을 예측하는 CNN을 구축하여, 마스크 3D 진폭을 재현하는 동시에 엄밀한 EM 시뮬레이션 대비 5000배 빠른 EUV 리소그래피 시뮬레이션을 달성한다.

## 주요 기여
1. EUV 마스크 3D 회절 진폭 예측 CNN 구축
2. 엄밀한 EM 시뮬레이션(FDTD/RCWA) 대비 5000배 가속 달성
3. 마스크 3D 진폭(M3D) 효과의 정확한 재현 검증
4. 2D 마스크 패턴 입력 → 복소 회절 진폭 출력 CNN 파이프라인
5. Tanabe 그룹의 EUV CNN 시뮬레이션 연구 초기 핵심 논문

## 모델 수식/아키텍처
- **CNN 구조**:
  - 입력: 2D EUV 마스크 패턴 (binary 또는 다층 재료 정보)
  - 컨볼루션 레이어: 마스크 패턴 공간 특징 추출
  - 출력: 복소 회절 진폭 스펙트럼 (진폭 + 위상)
- 학습 데이터: FDTD/RCWA로 계산된 다양한 마스크 패턴의 회절 진폭
- 속도: 학습 후 추론 시간 ≈ 엄밀 시뮬레이션 × (1/5000)
- 정확도: M3D 진폭 오차 < 수 % (패턴 유형에 따라 다름)

## 모델 유형
- [x] 광학
- [ ] 레지스트
- [x] ML/DL
- [x] 하이브리드 (CNN이 물리 기반 EM 시뮬레이션 대체)

## OPC 툴 구현 관련성
- SKOPC EUV M3D 계산의 핵심 가속 기술 — EM 시뮬레이터를 CNN으로 대체
- `2024_Tanabe_CNN_EUV_M3D_Pretrain.md`의 선행 연구
- `2023_Tanabe/2024_Tanabe` 시리즈: 2021(기초) → 2023(평가) → 2024(사전학습)
- TorchLitho 백엔드와 결합하여 미분 가능 EUV OPC 엔진 구현 가능

## 태그
`Model`, `EUV`, `CNN`, `M3D`, `FastSimulation`, `DiffractionAmplitude`, `Tanabe`, `JMM`, `SPIE`
