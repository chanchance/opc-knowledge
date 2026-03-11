# Neural-ILT 2.0: Migrating ILT to Domain-Specific and Multitask-Enabled Neural Network

## 메타데이터
- **저자**: Xue Liu, Kang Liu, Hao Geng, Bei Yu
- **연도**: 2022
- **게재지/학회**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD), Vol. 41, No. 8
- **DOI/URL**: https://ieeexplore.ieee.org/document/9526856; PDF: https://www.cse.cuhk.edu.hk/~byu/papers/J67-TCAD2022-Neural-ILT.pdf
- **인용수**: 80+

## 핵심 요약
ILT(Inverse Lithography Technology)를 도메인 특화 뉴럴 네트워크로 완전히 이전(migrate)한 Neural-ILT 2.0 논문. 기존 Neural-ILT (ICCAD 2020)를 확장하여, 리소그래피 도메인 지식을 사전학습(pretraining)에 명시적으로 통합하고, 마스크 예측·ILT 보정·복잡도 최적화를 멀티태스크로 처리하는 3-모듈 아키텍처를 제안한다. 단일 신경망으로 레이아웃에서 최적화된 마스크를 생성하며, 기존 gradient ILT 대비 수백 배 속도를 달성한다.

## 주요 기여
- 도메인 특화 사전학습(domain-specific pretraining) 기법 개발: 리소그래피 ILT 손실로 네트워크 수렴 가속
- 3-모듈 멀티태스크 아키텍처: UNet 백본 + ILT 보정 레이어 + 마스크 복잡도 정제 레이어
- 마스크 복잡도(mask complexity) 최적화를 학습 목표에 통합
- 기존 Neural-ILT 대비 정확도 및 수렴 속도 개선
- ICCAD 2013 벤치마크에서 state-of-the-art 성능 입증

## 모델 아키텍처/수식
**전체 파이프라인:**
```
Layout → [Module 1: UNet Backbone] → initial mask
       → [Module 2: ILT Correction Layer] → corrected mask
       → [Module 3: Mask Complexity Refinement] → final mask
```

**Module 1: UNet Backbone (도메인 특화 사전학습)**
- 인코더: Conv-BN-LeakyReLU × 8단
- 디코더: TransposeConv-BN-ReLU × 8단 (skip connections)
- 사전학습 손실:
```
L_pretrain = L_ILT + λ_c · L_complexity
L_ILT = ||Litho(M) - Z||²   (웨이퍼 이미지 vs 타겟)
L_complexity = Σ|∇M|         (마스크 엣지 길이 페널티)
```

**Module 2: ILT Correction Layer**
- 추가 gradient descent 단계 (학습 가능한 스텝 크기)
```
M_corrected = M_initial - α · ∇_M L_ILT(M_initial)
```
α: 학습 가능한 스칼라 파라미터

**Module 3: Mask Complexity Refinement**
- 이진화 및 불필요 feature 제거
- Threshold 기반 binarization + morphological 연산

**멀티태스크 전체 손실:**
```
L_total = w₁·L_print + w₂·L_EPE + w₃·L_complexity
```
- L_print: 프린팅 정확도 (픽셀 단위 L2)
- L_EPE: Edge Placement Error
- L_complexity: 마스크 복잡도 (Sub-Resolution Assist Feature 포함)

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 `skopc/modeling/gnn/` 모듈과 아키텍처 비교 연구에 중요. GNN 기반 세그먼트 변위 예측과 Neural-ILT의 픽셀 기반 마스크 최적화는 상호 보완적 접근법. ILT Correction Layer의 gradient descent 통합은 SKOPC에서 GNN 예측 후 fine-tuning 단계로 활용 가능. 특히 도메인 특화 사전학습 기법은 SKOPC GNN 모델의 초기 가중치 생성에 적용 가능.

## 참고문헌 (핵심)
- Yang, H. et al., "GAN-OPC: Mask optimization with lithography-guided GANs," DAC 2018 / TCAD 2020
- Liu, X. et al., "Neural-ILT: Migrating ILT to neural networks for mask synthesis," ICCAD 2020
- Isola, P. et al., "Image-to-image translation with CGANs," CVPR 2017
- Ronneberger, O. et al., "U-Net: CNNs for biomedical image segmentation," MICCAI 2015
- Gao, J. et al., "Bidirectional square matching for OPC correction," IEEE Trans. CAD 2012

## 태그
`Model`, `OPC`, `ILT`, `NeuralNetwork`, `DeepLearning`, `UNet`, `MaskOptimization`, `DomainSpecific`, `Multitask`, `TCAD`, `ICCAD`, `Pretraining`
