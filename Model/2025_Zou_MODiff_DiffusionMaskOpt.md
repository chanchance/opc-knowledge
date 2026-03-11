# MODiff: Layout-guided Mask Optimization via Diffusion Model

## 메타데이터
- **저자**: Ningmu Zou (Nanjing University School of Integrated Circuits)
- **연도**: 2025
- **게재지/학회**: SPIE Advanced Lithography + Patterning 2025, Presentation 13980-31
- **DOI/URL**: https://spie.org/advanced-lithography/presentation/MODiff-Layout-guided-mask-optimization-via-diffusion-model/13980-31
- **인용수**: 신규 (2025년 발표)

## 핵심 요약
확산 모델(Diffusion Model)을 최초로 OPC 마스크 최적화에 적용한 논문. 타겟 레이아웃에 의해 가이드되는 "노이즈-to-마스크" 디노이징(denoising) 과정으로 고품질 마스크를 생성한다. Forward 리소그래피 시뮬레이터를 정확도 보장에 통합하고, 안정적인 학습을 위해 코사인 스케줄러(cosine scheduler)를 사용한다. ICCAD 2013 데이터셋에서 via 레이어를 포함한 마스크 정밀도와 엣지 부드러움(edge smoothness) 면에서 기존 최신 기법을 능가한다.

## 주요 기여
- 확산 모델을 OPC 마스크 최적화에 최초 적용
- 레이아웃 조건부 디노이징으로 고품질, 규칙적인 마스크 생성
- Forward 리소그래피 시뮬레이터 통합으로 물리적 정확도 보장
- 코사인 노이즈 스케줄러로 학습 안정성 향상
- ICCAD 2013 벤치마크에서 마스크 정밀도 및 엣지 품질 state-of-the-art

## 모델 아키텍처/수식
**확산 모델 기반 마스크 생성 파이프라인:**

**Forward 확산 과정 (노이즈 추가):**
```
q(M_t | M_{t-1}) = N(M_t; √(1-β_t)·M_{t-1}, β_t·I)

q(M_t | M_0) = N(M_t; √ᾱ_t·M_0, (1-ᾱ_t)·I)
ᾱ_t = Π_{s=1}^{t} (1-β_s)   (코사인 스케줄러)
```

M_0: 최적 ILT 마스크 (ground truth)
M_T: 순수 가우시안 노이즈 (T 스텝 후)

**Reverse 디노이징 과정 (마스크 생성):**
```
p_θ(M_{t-1} | M_t, L) = N(M_{t-1}; μ_θ(M_t, t, L), Σ_θ(M_t, t, L))
```
L: 타겟 레이아웃 (conditioning)

**디노이징 네트워크 ε_θ (UNet 기반):**
```
Input: (M_t, t, L)   # 노이즈 마스크, 타임스텝, 레이아웃
Output: ε_pred       # 예측 노이즈
```
- 레이아웃 L은 cross-attention으로 conditioning
- 타임스텝 t는 sinusoidal embedding으로 인코딩

**리소그래피 시뮬레이터 통합 (Guidance):**
```
∇_{M_t} log p(L | M_t) ≈ -1/σ² · ∂||Litho(M̃_0) - L||²/∂M_t
```
여기서 M̃_0 = (M_t - √(1-ᾱ_t)·ε_θ) / √ᾱ_t (현재 단계의 x_0 추정)

**학습 손실:**
```
L_simple = E_{t, M_0, ε}[||ε - ε_θ(M_t, t, L)||²]
L_litho = ||Litho(M̃_0) - L||²
L_total = L_simple + λ·L_litho
```

**코사인 노이즈 스케줄러:**
```
β_t = 1 - (ᾱ_t / ᾱ_{t-1})
ᾱ_t = cos²(π·t / (2T) · (s+1)/(1+s))   (s=0.008)
```

**추론 (Inference):**
```
M_T ~ N(0, I)
for t = T, T-1, ..., 1:
    M_{t-1} = Denoise(M_t, t, L) + Litho_guidance
M_0 → binarize → final mask
```

**ICCAD 2013 벤치마크 성능:**
- Mask Precision: GAN-OPC 대비 +5% 향상
- Edge Smoothness: Neural-ILT 대비 +8% 향상
- Via layer 포함 전 레이어 우수한 성능

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 다음 세대 마스크 최적화 모듈로 고려 가능. 현재 GNN 기반 세그먼트 변위 예측 방식과 달리, 확산 모델은 마스크 전체 패턴을 생성적으로 최적화한다. `skopc/modeling/gnn/` 모듈의 대안 또는 후처리(post-processing) 단계로 통합 가능. 확산 모델의 규칙적인 마스크 생성 특성은 마스크 제조 가능성(mask manufacturability) 향상에 유리. PyTorch 기반으로 TorchLitho와 통합 용이.

## 참고문헌 (핵심)
- Ho, J. et al., "Denoising diffusion probabilistic models (DDPM)," NeurIPS 2020
- Song, Y. et al., "Score-based generative modeling through SDEs," ICLR 2021
- Dhariwal, P. and Nichol, A., "Diffusion models beat GANs," NeurIPS 2021
- Yang, H. et al., "GAN-OPC," DAC 2018
- Liu, X. et al., "Neural-ILT 2.0," TCAD 2022

## 태그
`Model`, `OPC`, `DiffusionModel`, `MaskOptimization`, `GenerativeAI`, `DDPM`, `ILT`, `SPIE`, `Denoising`, `LayoutGuided`, `CosineScheduler`, `PhysicsGuided`
