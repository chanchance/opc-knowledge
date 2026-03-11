# GAN-OPC: Mask Optimization with Lithography-guided Generative Adversarial Nets

## 메타데이터
- **저자**: Haoyu Yang, Shuhe Li, Yuzhe Ma, Bei Yu, Evangeline F.Y. Young
- **연도**: 2018 (DAC), 2020 (TCAD 저널판)
- **게재지/학회**: ACM/IEEE Design Automation Conference (DAC 2018); IEEE Transactions on Computer-Aided Design (TCAD 2020)
- **DOI/URL**: https://doi.org/10.1145/3195970.3196056 (DAC); https://ieeexplore.ieee.org/document/8823939 (TCAD)
- **인용수**: 300+

## 핵심 요약
GAN(Generative Adversarial Network)을 최초로 OPC 마스크 최적화에 적용한 선구적 논문. 레이아웃(타겟 패턴)에서 최적화된 마스크 패턴으로의 매핑을 GAN으로 학습한다. 기존 gradient 기반 ILT가 수백 번의 반복 최적화를 요구하는 것과 달리, GAN-OPC는 학습 후 단일 순전파(forward pass)로 마스크를 생성하여 수십~수백 배의 속도 향상을 달성한다. 리소그래피 물리 시뮬레이터를 판별자(discriminator) 학습에 통합하여 물리적 정확도를 보장한다.

## 주요 기여
- OPC 마스크 최적화에 GAN 최초 적용
- 리소그래피 시뮬레이터를 GAN 학습 루프에 통합 (physics-guided training)
- 기존 ILT 대비 수십 배 이상 속도 향상
- L2 손실 + 적대적 손실(adversarial loss) + 리소그래피 손실의 복합 목적함수 설계
- 다양한 패턴 복잡도에서 일반화 성능 입증

## 모델 아키텍처/수식
**생성자(Generator) G:**
- U-Net 구조 기반 (Encoder-Decoder with skip connections)
- 입력: 타겟 레이아웃 이미지 (binary, 512×512)
- 출력: 연속값 마스크 패턴 → 이진화하여 최종 마스크

**판별자(Discriminator) D:**
- PatchGAN 구조 (국소 영역 판별)
- 실제 ILT 최적화 마스크 vs. 생성 마스크 구별

**목적함수:**
```
L_total = λ₁·L_adv + λ₂·L_L2 + λ₃·L_litho

L_adv = E[log D(mask_real)] + E[log(1 - D(G(layout)))]

L_L2 = ||G(layout) - mask_ILT||²

L_litho = ||Litho(G(layout)) - target||²
```

여기서 Litho(·)는 미분 가능한 리소그래피 시뮬레이터.

**리소그래피 가이드 학습:**
```
mask_output = G(layout)
wafer_image = Litho(mask_output)  # forward lithography simulation
EPE = ||wafer_image - target_layout||
```

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 GNN-OPC 모듈(`skopc/modeling/gnn/`) 개발 시 참조할 핵심 논문. GAN-OPC의 U-Net 생성자 구조는 픽셀 단위 마스크 최적화에 적합하며, GNN 기반 세그먼트 변위 예측과 상호 보완적이다. 리소그래피 손실(L_litho)을 학습에 통합하는 방식은 SKOPC의 `LithoEngine`을 PyTorch autograd와 연결하는 방식으로 구현 가능. 현재 SKOPC는 GNN 기반이지만, 픽셀 단위 전처리 단계에 GAN 접근법 통합 가능.

## 참고문헌 (핵심)
- Goodfellow, I. et al., "Generative adversarial nets," NeurIPS 2014
- Ronneberger, O. et al., "U-Net: Convolutional networks for biomedical image segmentation," MICCAI 2015
- Isola, P. et al., "Image-to-image translation with conditional adversarial networks," CVPR 2017
- Gao, J. et al., "Optical proximity correction with linear regression," IEEE Trans. Semicond. Manuf. 2008
- Yu, P. and Pan, D.Z., "True process variation aware OPC," JM3 2007

## 태그
`Model`, `OPC`, `GAN`, `DeepLearning`, `MaskOptimization`, `ILT`, `UNet`, `PhysicsGuided`, `Lithography`, `GenerativeModel`, `TCAD`
