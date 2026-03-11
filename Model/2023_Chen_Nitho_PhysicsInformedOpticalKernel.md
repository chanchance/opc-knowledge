# Physics-Informed Optical Kernel Regression Using Complex-valued Neural Fields

## 메타데이터
- **저자**: Guojin Chen, Haoyu Yang, Bei Yu, Martin D.F. Wong (CUHK, NVIDIA)
- **연도**: 2023
- **게재지/학회**: ACM/IEEE Design Automation Conference (DAC 2023); arXiv:2303.08435
- **DOI/URL**: https://doi.org/10.1145/3489517.XXXXXX; https://arxiv.org/abs/2303.08435; PDF: https://www.cse.cuhk.edu.hk/~byu/papers/C168-DAC2023-Nitho.pdf
- **인용수**: 40+

## 핵심 요약
NeRF(Neural Radiance Field) 에서 영감을 받은 물리 정보 내재형 리소그래피 신경망 Nitho를 제안한 논문. 리소그래피 모델을 비파라메트릭 마스크 연산과 광학 커널을 포함한 학습된 TCC 스펙트럼으로 분해한다. 복소수 값(complex-valued) 신경 필드를 최적화하여 좌표에서 TCC 스펙트럼을 예측하는 광학 커널 회귀를 수행한다. 소규모 학습 데이터셋으로 적은 파라미터를 사용하면서 우수한 일반화 성능을 보이며, 다양한 리소그래피 시스템을 정확히 재현한다.

## 주요 기여
- NeRF에서 영감받은 복소수 신경 필드(complex-valued neural fields)로 TCC 스펙트럼 학습
- 리소그래피 모델을 마스크 연산 + 광학 커널(TCC)로 물리적으로 분해
- 소규모 데이터로 효율적인 리소그래피 시스템 역설계(reverse engineering)
- 광원/동공/리소그래피 정보가 담긴 광학 커널 자동 학습
- 뛰어난 일반화: 학습 미포함 조명/마스크 조건으로 일반화

## 모델 아키텍처/수식
**리소그래피 모델 분해:**

Hopkins TCC 기반 이미지 강도:
```
I(x) = ∫∫ TCC(f₁, f₂) · M(f₁) · M*(f₂) · exp(j2π(f₁-f₂)x) df₁df₂
```

Nitho의 분해:
- 비파라메트릭 마스크 연산: M(f) 계산 (Fourier transform, 학습 불필요)
- 학습된 광학 커널: TCC(f₁, f₂) → 복소수 신경 필드로 학습

**Nitho 복소수 신경 필드:**

TCC를 좌표 (f₁, f₂)의 함수로 신경 필드로 표현:
```
TCC_pred(f₁, f₂) = NeRF_θ(f₁, f₂)
```

복소수 출력 신경망:
```
Input: (f₁_real, f₁_imag, f₂_real, f₂_imag)
       ↓
[Positional Encoding (Fourier features)]
  γ(f) = [cos(2πBf), sin(2πBf)]  (B: 랜덤 주파수 행렬)
       ↓
[MLP layers with complex activation]
  z^(l+1) = σ_c(W^(l)·z^(l) + b^(l))
  σ_c(z) = ReLU(Re(z)) + j·ReLU(Im(z))  (복소수 ReLU)
       ↓
Output: TCC_pred(f₁, f₂) ∈ ℂ
```

**물리적 제약 (Physics-Informed):**
TCC의 에르미트(Hermitian) 대칭성:
```
TCC(f₁, f₂) = TCC*(f₂, f₁)
```
TCC의 반정부정(NSPD) 조건:
```
∫ TCC(f₁, f₂) · g(f₁) · g*(f₂) df₁df₂ ≥ 0, ∀g
```
이를 손실 함수에 정규화로 포함:
```
L_physics = ||TCC_pred - TCC_pred*^T||² + max(0, -λ_min(TCC_pred))
```

**학습:**
```
L_total = ||I_pred - I_GT||² + λ·L_physics
```
I_pred = I(x; TCC_pred, M)  (예측 TCC로 계산한 이미지)

**SVD 기반 커널 추출:**
```
TCC_pred = Σₙ σₙ · uₙ · vₙ†   (SVD)
→ n개 coherent kernel: {√σₙ · uₙ} (Forward 시뮬레이션에 활용)
```

**성능:**
- 데이터 효율: 기존 방법 대비 1/10 데이터로 동등 성능
- 일반화: 미학습 조명 조건에서 RMSE -30%
- 속도: 전통 TCC 계산 대비 5× 빠름

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 `LithoEngine` 내 TCC 계산을 Nitho 방식으로 대체/보완 가능. 특히 새로운 리소그래피 장비(스캐너) 도입 시, 소량의 인쇄 결과만으로 TCC를 자동 학습하는 역설계에 활용 가능. `recipes/example_arfimm.yaml`의 광학 파라미터(NA, sigma, aberration)를 Nitho가 자동으로 추출하는 보정 방법으로 참조. 복소수 신경 필드는 PyTorch의 complex tensor 지원으로 구현 가능.

## 참고문헌 (핵심)
- Hopkins, H.H., "On the diffraction theory of optical images," Proc. R. Soc. London A (1953)
- Mildenhall, B. et al., "NeRF: Representing scenes as neural radiance fields," ECCV 2020
- Tancik, M. et al., "Fourier features let networks learn high frequency functions," NeurIPS 2020
- Chen, G. et al., "Open-source differentiable lithography framework," arXiv:2409.15306 (2024)
- Yang, H. et al., "Dual-band optics-inspired NN," DAC 2022

## 태그
`Model`, `OPC`, `OpticalModel`, `TCC`, `NeRF`, `NeuralFields`, `ComplexValued`, `PhysicsInformed`, `KernelRegression`, `DAC`, `CUHK`, `NVIDIA`, `DataEfficient`, `Generalization`
