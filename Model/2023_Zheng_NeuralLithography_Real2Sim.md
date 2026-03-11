# Neural Lithography: Close the Design-to-Manufacturing Gap in Computational Optics with a 'Real2Sim' Learned Photolithography Simulator

## 메타데이터
- **저자**: Cheng Zheng, Guangyuan Zhao, Peter T.C. So (MIT)
- **연도**: 2023
- **게재지/학회**: SIGGRAPH Asia 2023; arXiv:2309.17343
- **DOI/URL**: https://doi.org/10.1145/3610548.3618251; https://arxiv.org/abs/2309.17343; GitHub: https://github.com/Neural-Litho/Neural-Lithography
- **인용수**: 60+

## 핵심 요약
계산 광학(computational optics)의 설계-제조 격차(design-to-manufacturing gap)를 해소하기 위한 신경망 리소그래피 프레임워크를 제안한 논문. 기존 광학 설계 접근법이 제조 공정의 수치 모델링을 무시하여 설계와 제작된 광학 소자 간에 큰 성능 편차가 발생하는 문제를 해결한다. 물리 정보 모델링과 실험 데이터 기반 학습을 결합한 'Real2Sim' 포토리소그래피 시뮬레이터를 사전 학습하고, 이를 모델 기반 광학 설계 루프에 통합하여 제조 가능성을 설계 단계에서 정규화한다.

## 주요 기여
- 'Real2Sim' 접근법: 실제 리소그래피 시스템의 특성을 신경망으로 학습
- 물리 기반 모델 + 데이터 기반 학습의 하이브리드 포토리소그래피 시뮬레이터
- 완전 미분 가능한 설계 프레임워크로 end-to-end 최적화
- 제조 가능성(fabrication feasibility)을 설계 목적함수의 정규화로 통합
- 홀로그래픽 광학 소자(HOE)와 다중 레벨 회절 렌즈(MDL) 제작에서 성능 입증

## 모델 아키텍처/수식
**Real2Sim 포토리소그래피 시뮬레이터:**

물리 기반 기저 모델:
```
I_phys(x) = |h_coherent ⊗ mask(x)|²   (단순화된 물리 모델)
```

신경망 보정 (시스템 특이적 편차 학습):
```
I_sim(x) = I_phys(x) + NN_θ(I_phys(x), mask(x))
```
NN_θ: 실제 시스템의 비이상적 효과(수차, 비선형성 등) 보정

**Real2Sim 학습:**
```
L_sim = Σᵢ ||I_sim(mask_i) - I_real,i||²
```
여기서 I_real,i: 실제 리소그래피 시스템으로 제작한 패턴의 측정값

**완전 미분 가능 설계 루프:**
```
Optical Design Objective: L_opt(design)
Manufacturing Constraint: L_mfg = ||I_sim(mask(design)) - design||²

Total: L_total = L_opt + λ·L_mfg
∂L_total/∂design = ∂L_opt/∂design + λ·∂L_mfg/∂design  (autograd)
```

**두 광자 리소그래피(Two-Photon Lithography) 적용:**
- 비선형 광반응: I_resist ∝ I²  (이광자 흡수)
- 3D 레지스트 프로파일 시뮬레이션
- 나노스케일 해상도 패턴 제작

**응용 사례:**
1. 홀로그래픽 광학 소자(HOE):
   ```
   target: phase hologram H(x,y)
   fabricated: photoresist profile → HOE
   Neural Litho로 제작 시 회절 효율 30% 향상
   ```

2. 다중 레벨 회절 렌즈(MDL):
   ```
   target: focusing lens L(x,y)
   fabricated: multilevel relief lens
   Neural Litho로 제작 시 집광 효율 25% 향상
   ```

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 모델 보정(calibration) 방향과 직접 관련. Real2Sim 접근법을 SKOPC에 적용하면, CD-SEM 측정 데이터에서 리소그래피 시스템의 특이적 특성(aberration, flare 등)을 신경망으로 학습하여 더 정확한 `LithoEngine` 보정이 가능. 특히 새로운 스캐너 도입 시 소량의 인쇄 데이터만으로 시뮬레이터를 보정하는 방법으로 활용. SKOPC의 `recipes/` 내 calibration workflow에 통합 가능.

## 참고문헌 (핵심)
- Chen, G. et al., "Open-source differentiable lithography," arXiv:2409.15306 (2024)
- Mildenhall, B. et al., "NeRF," ECCV 2020
- Chen, G. et al., "Nitho: Physics-informed optical kernel regression," DAC 2023
- Goodman, J.W., "Introduction to Fourier optics," Roberts & Company (2005)

## 태그
`Model`, `OPC`, `Real2Sim`, `NeuralLithography`, `Calibration`, `PhysicsInformed`, `DataDriven`, `TwoPhoton`, `HOE`, `MDL`, `DesignToManufacturing`, `SIGGRAPH`, `MIT`
