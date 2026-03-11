# LithoGAN: End-to-End Lithography Modeling with Generative Adversarial Networks

## 메타데이터
- **저자**: Chenxi Ye, Bei Yu, Evangeline F.Y. Young
- **연도**: 2019
- **게재지/학회**: ACM/IEEE Design Automation Conference (DAC 2019)
- **DOI/URL**: https://ieeexplore.ieee.org/document/8806997
- **인용수**: 120+

## 핵심 요약
GAN을 이용한 end-to-end 리소그래피 모델링 프레임워크 LithoGAN을 제안한 논문. 마스크 패턴을 입력으로 받아 웨이퍼 상의 레지스트 이미지를 직접 예측한다. 기존 물리 기반 시뮬레이터(Hopkins 모델 + 레지스트 모델)의 계산 병목을 GAN으로 대체하여 정확도를 유지하면서 대폭적인 속도 향상을 달성한다. Conditional GAN (CGAN) 구조를 사용하며, 256×256 해상도의 타일 단위 처리를 통해 full-chip 적용 가능성을 시연한다.

## 주요 기여
- GAN 기반 리소그래피 forward 모델 (마스크 → 웨이퍼 이미지) 구현
- Conditional GAN(CGAN) 구조로 마스크 조건부 웨이퍼 이미지 생성
- 물리 시뮬레이터 대비 100~1000배 속도 향상
- 정확도-속도 트레이드오프 정량적 분석
- full-chip 스케일 적용을 위한 타일 기반 처리 파이프라인 제안

## 모델 아키텍처/수식
**전체 구조: Conditional GAN (CGAN)**
- 입력: 마스크 이미지 (binary, 256×256)
- 출력: 웨이퍼 레지스트 이미지 (grayscale, 256×256)

**생성자(Generator):**
- 완전 합성곱 네트워크 (Fully Convolutional Network, FCN)
- Encoder: Conv→BN→LeakyReLU 블록 × 8
- Decoder: TransposeConv→BN→ReLU 블록 × 8 (U-Net skip connections)
- 최종 활성화: Tanh

**판별자(Discriminator):**
- 합성곱 신경망 (Convolutional Neural Network)
- 입력: (마스크, 웨이퍼 이미지) 쌍
- PatchGAN 방식으로 국소 패치 단위 판별

**목적함수:**
```
L_CGAN(G, D) = E[log D(mask, wafer_real)]
             + E[log(1 - D(mask, G(mask)))]

L_L1 = E[||wafer_real - G(mask)||₁]

L_total = L_CGAN + λ·L_L1
```
λ = 100 (L1 손실 가중치)

**타일 기반 처리:**
```
full_chip → tiles (256×256, overlap 32px)
→ LithoGAN inference per tile
→ stitch tiles → full wafer image
```

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 `LithoEngine` 가속화 대안으로 활용 가능. 현재 SKOPC는 TorchLitho/TorchResist 기반 물리 시뮬레이션을 사용하지만, LithoGAN 방식으로 학습된 surrogate 모델을 추가하면 OPC 루프의 반복 시뮬레이션 속도를 크게 높일 수 있다. `skopc/modeling/gnn/` 모듈에서 GNN 세그먼트 변위 예측 전 빠른 웨이퍼 이미지 예측에 활용 가능. 특히 PWO(공정 윈도우 최적화)에서 수천 번의 시뮬레이션이 필요할 때 surrogate 모델로 유용.

## 참고문헌 (핵심)
- Yang, H. et al., "GAN-OPC: Mask optimization with lithography-guided generative adversarial nets," DAC 2018
- Isola, P. et al., "Image-to-image translation with conditional adversarial networks," CVPR 2017
- Goodfellow, I. et al., "Generative adversarial nets," NeurIPS 2014
- Ma, X. et al., "Lithography friendly cloudiness and corner rounding effects modeling," SPIE 2013

## 태그
`Model`, `OPC`, `GAN`, `LithoGAN`, `LithographySimulation`, `DeepLearning`, `ForwardModel`, `SurrogateModel`, `CGAN`, `FullChip`, `DAC`
