# Generic Lithography Modeling with Dual-band Optics-Inspired Neural Networks

## 메타데이터
- **저자**: Haoyu Yang, Zongyi Li, Kumara Sastry, Saumyadip Mukhopadhyay, Mark Kilgard, Anima Anandkumar, Brucek Khailany, Vivek Singh, Mark Haoxing Ren
- **연도**: 2022
- **게재지/학회**: ACM/IEEE Design Automation Conference (DAC 2022); arXiv:2203.08616
- **DOI/URL**: https://doi.org/10.1145/3489517.3530580; https://arxiv.org/abs/2203.08616
- **인용수**: 80+

## 핵심 요약
NVIDIA 연구팀이 제안한 광학 물리를 내재화한 이중 대역(dual-band) 신경망 기반 리소그래피 모델링 프레임워크. 리소그래피 광학계의 물리적 원리(Hopkins TCC 모델의 주파수 대역 특성)를 신경망 아키텍처에 직접 반영하여, 기존 ML 방법 대비 20배 작은 모델 크기와 85배 시뮬레이션 속도 향상을 달성한다. 1nm²/pixel 해상도에서 via/metal 레이어 컨투어 시뮬레이션을 최초로 공개 발표했으며, 전통적인 리소그래피 시뮬레이터 대비 1% 정확도 손실만으로 85배 속도를 달성한다.

## 주요 기여
- 광학 물리(TCC 이중 대역 구조)를 신경망 아키텍처에 내재화
- 기존 ML 방법 대비 20배 모델 크기 축소
- 전통 시뮬레이터 대비 85배 속도 향상 (1% 정확도 손실)
- 1nm²/pixel 해상도 via/metal 레이어 컨투어 시뮬레이션 최초 공개
- 임의 타일 크기 처리 가능 (어떤 타일 크기도 지원)
- NVIDIA cuLitho 플랫폼의 기반 기술 중 하나

## 모델 아키텍처/수식
**핵심 아이디어: 이중 대역 (Dual-band) 분해**

TCC 모델의 주파수 특성에서 착안:
리소그래피 이미지 = 저주파 성분 + 고주파 성분
```
I(x) = I_low(x) + I_high(x)
```

**Dual-band Neural Network 구조:**
```
Input: Mask tile M
↓
[Low-freq Branch]        [High-freq Branch]
Conv(large kernel)  +   Conv(small kernel)
↓                       ↓
Low-freq features   High-freq features
↓                       ↓
[Fusion Module] → Predicted Wafer Image
```

**저주파 브랜치 (Long-range interactions):**
- 큰 수용 영역(receptive field) 커널
- TCC의 주요(dominant) 고유 커널 모방
- Fourier Neural Operator (FNO) 레이어로 전역 의존성 포착:
  ```
  y_low = IFFT(R_θ · FFT(x))
  ```
  R_θ: 학습 가능한 주파수 공간 필터

**고주파 브랜치 (Short-range interactions):**
- 작은 수용 영역 커널 (지역 패턴 특징)
- TCC의 고차(higher-order) 고유 커널 모방
- 일반 합성곱 레이어

**물리 기반 특징 (Optics-Inspired):**
```
H_eff(f) = H_low(f) + H_high(f)
I(x) ≈ Σₙ,low λₙ|φₙ ⊗ m|² + Σₙ,high λₙ|φₙ ⊗ m|²
```
저주파/고주파 TCC 고유 커널을 각 브랜치로 분리 근사

**손실 함수:**
```
L = ||I_pred - I_GT||₂ + λ_contour·L_contour + λ_grad·||∇I_pred - ∇I_GT||₂
```

**성능 (NVIDIA 내부 벤치마크):**
- 속도: 전통 시뮬레이터 대비 85×
- 정확도: 1% 이내 오차
- 모델 크기: 기존 ML 방법 대비 1/20
- 해상도: 1nm²/pixel (via/metal 레이어)

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC에서 TorchLitho 기반 시뮬레이션의 대안적 가속 방법으로 참조. Dual-band 구조는 TCC SVD 분해의 신경망 구현이므로, SKOPC `LithoEngine` 가속 시 이 아키텍처를 surrogate 모델로 활용 가능. 특히 PWO(공정 윈도우 최적화)에서 수천 번의 시뮬레이션이 필요할 때 85× 속도 향상이 중요. NVIDIA cuLitho와의 통합 가능성도 고려.

## 참고문헌 (핵심)
- Hopkins, H.H., "On the diffraction theory of optical images," Proc. R. Soc. London A (1953)
- Li, Z. et al., "Fourier neural operator for parametric PDEs," ICLR 2021
- Yang, H. et al., "GAN-OPC," DAC 2018
- Chen, G. et al., "DAMO," ICCAD 2020
- NVIDIA cuLitho: https://developer.nvidia.com/culitho

## 태그
`Model`, `OPC`, `DualBand`, `NeuralNetwork`, `PhysicsInspired`, `LithographySimulation`, `FNO`, `FourierNeuralOperator`, `NVIDIA`, `cuLitho`, `SpeedUp`, `TCC`, `DAC`
