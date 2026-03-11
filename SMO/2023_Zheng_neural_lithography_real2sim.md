# Neural Lithography: Close the Design-to-Manufacturing Gap with a Real2Sim Learned Photolithography Simulator

## 메타데이터
- **저자**: Cheng Zheng, Guangyuan Zhao, Peter T.C. So
- **연도**: 2023
- **게재지/학회**: SIGGRAPH Asia 2023, arXiv:2309.17343
- **DOI/URL**: https://arxiv.org/abs/2309.17343
- **인용수**: SIGGRAPH Asia 2023 다수 인용

## 핵심 요약
광리소그래피 시뮬레이터를 광학 설계 워크플로우에 통합하는 Neural Lithography 프레임워크를 제안한 논문. 물리 정보 모델링과 실험 데이터 기반 학습을 결합한 Real2Sim 접근으로 시뮬레이터를 제조 가능성에 대한 정규화기(regularizer)로 활용한다. 홀로그래픽 광학 소자(HOE)와 다층 회절 렌즈(MDL)에서 설계-제조 간 성능 격차를 현저히 줄인다.

## 주요 기여
- 광리소그래피 시뮬레이션과 광학 설계 최적화를 결합한 최초의 완전 미분 가능 설계 프레임워크
- 물리 원리와 머신러닝을 혼합한 하이브리드 Real2Sim 모델링 접근
- 제조 가능성 정규화기로서의 리소그래피 시뮬레이터 활용
- 2광자 리소그래피(two-photon lithography)에서 HOE 및 MDL 실증
- 설계-제조 성능 격차 대폭 감소

## 알고리즘/수식
- **Real2Sim 리소그래피 시뮬레이터**:
  - 입력: 설계 패턴 D (그레이스케일 또는 이진)
  - 출력: 제조 후 실제 형상 예측 D̂
  - 모델: D̂ = f_NN(D; θ_litho), θ_litho는 실험 데이터로 학습

- **물리 정보 하이브리드 모델**:
  - 물리 기반: 광학 근접 효과 모델 (Abbe 적분)
  - 데이터 기반: 잔차 오차 신경망 보정
  - D̂ = D_physics + ΔD_NN

- **제조 인식 광학 설계 최적화**:
  - min_{φ} L_optical(forward(f_NN(φ))) + λ·L_reg(f_NN(φ))
  - φ: 설계 파라미터 (위상, 높이 등)
  - f_NN: 미분 가능 리소그래피 시뮬레이터 (역전파 가능)
  - L_reg: 제조 가능성 정규화 손실

- **2광자 리소그래피 적용**:
  - 포토레지스트 감광 모델 + 현상 모델 학습
  - 3D 구조물 (DOE, 렌즈) 형상 예측

- **적용 사례**:
  - HOE (Holographic Optical Element): 회절 효율 향상
  - MDL (Multi-level Diffractive Lens): 초점 성능 향상

## OPC 툴 구현 관련성
SKOPC의 TorchLitho/TorchResist 기반 캘리브레이션 모듈과 직접 연관. Real2Sim 접근법은 SKOPC의 `skopc/modeling/calibration.py`에서 실험 SEM 데이터와 시뮬레이션 모델 정렬에 참조 가능. 완전 미분 가능 파이프라인은 SKOPC의 GNN-OPC 훈련 루프와 동일한 원리. HOE/MDL 설계 최적화 방법론은 SKOPC SMO에서 소스 형상 최적화에 응용 가능.

## 참고문헌 (핵심)
- Goodman, "Introduction to Fourier Optics" — 광학 기초
- Ho et al., DDPM (2020) — 생성 모델 관련
- TorchLitho 관련 미분 가능 리소그래피 프레임워크 논문들
- 2광자 리소그래피 공정 문헌

## 태그
`neural-lithography`, `real2sim`, `photolithography-simulator`, `fabrication-aware`, `differentiable`, `holographic`, `diffractive-lens`, `two-photon`, `SIGGRAPH`, `2023`, `arxiv`
