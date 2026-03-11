# GAN-OPC: Mask Optimization With Lithography-Guided Generative Adversarial Nets

## 메타데이터
- **저자**: Haoyu Yang, Shuhe Li, Zihao Deng, Yuzhe Ma, Bei Yu, Evangeline F. Y. Young
- **연도**: 2020 (DAC 2018 발표 → TCAD 2020 확장)
- **게재지/학회**: IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems (TCAD), Vol. 39, No. 10, pp. 2822-2834
- **DOI/URL**: https://ieeexplore.ieee.org/document/8823939 / https://dl.acm.org/doi/10.1145/3195970.3196056
- **인용수**: 300+ (고인용 논문)

## 핵심 요약
GAN-OPC는 생성적 적대 신경망(GAN)을 활용하여 전통적인 반복적 OPC 최적화를 대체하는 딥러닝 기반 마스크 최적화 프레임워크다. 리소그래피 물리 제약을 GAN 아키텍처에 내재화하여, 설계 레이아웃에서 최적 마스크로의 직접 매핑을 학습한다. ILT(역리소그래피 기술)와의 공동 사전학습(pretraining) 전략으로 수렴성을 개선하며, 전통 OPC 대비 대폭 단축된 연산 시간으로 유사하거나 우수한 마스크 품질을 달성한다.

## 주요 기여
- **리소그래피 유도 GAN**: 리소그래피 물리 제약을 GAN 손실 함수에 직접 통합
- **ILT 공동 사전학습**: GAN 수렴 가속을 위한 ILT 기반 사전학습 전략 제안
- **직접 마스크 생성**: 반복적 OPC 단계 없이 타겟 패턴에서 최적 마스크 직접 생성
- **연산 효율성**: 전통 ILT/MBOPC 대비 수십~수백 배 속도 향상

## Recipe/Process Flow 상세

### GAN-OPC 마스크 최적화 플로우

```
사전학습 단계 (Pretraining Phase):
  타겟 레이아웃 → ILT 최적화 → 마스크 레이블 생성
  타겟-마스크 쌍으로 생성기(G) 사전학습

적대적 학습 단계 (GAN Training):
  [생성기 G]
    입력: 타겟 레이아웃 패턴
    출력: 최적화된 마스크 패턴
    손실: L_adv + L_litho + L_rec
  [판별기 D]
    입력: (타겟, 마스크) 쌍 (진짜 vs 생성)
    출력: 진위 판별 점수

추론 단계 (Inference):
  새 타겟 레이아웃 → G(레이아웃) → 마스크 → (필요시 소수 OPC 반복) → 최종 마스크
```

### GAN 손실 함수
$$\mathcal{L}_{GAN} = \mathcal{L}_{adv} + \lambda_1 \mathcal{L}_{litho} + \lambda_2 \mathcal{L}_{rec}$$

- **$\mathcal{L}_{adv}$**: 표준 GAN 적대적 손실 (진짜 마스크 분포 학습)
- **$\mathcal{L}_{litho}$**: 리소그래피 물리 손실 (생성 마스크의 인쇄 품질 평가)
  $$\mathcal{L}_{litho} = \|I(G(T)) - T\|^2$$
  여기서 I(·)는 리소그래피 이미징 함수, T는 타겟 패턴
- **$\mathcal{L}_{rec}$**: 재구성 손실 (생성 마스크와 ILT 기준 마스크의 유사도)

### 아키텍처 상세
- **생성기(G)**: U-Net 기반 인코더-디코더 (스킵 커넥션 포함)
  - 인코더: Conv → BatchNorm → LeakyReLU (6단계)
  - 디코더: TransposeConv → BatchNorm → ReLU (6단계)
  - 출력: 이진 마스크 패턴 (sigmoid 활성화)
- **판별기(D)**: PatchGAN 구조 (패치 단위 진위 판별)

### 학습 데이터
- 리소그래피 시뮬레이션으로 생성된 타겟-마스크 쌍 (~4,000 디자인)
- 다양한 VLSI 레이아웃 패턴 포함 (라인, 공간, 코너, 2D 패턴)
- ILT로 생성된 레퍼런스 마스크가 레이블로 사용

### OPC 레시피 관련 파라미터
- 타일 크기: 레이아웃을 고정 크기 타일로 분할하여 처리
- 리소그래피 모델: 부분 간섭성 이미징 (Hopkins 방정식)
- 평가 지표: EPE, PVB, L₂ 손실

## OPC 툴 구현 관련성
GAN-OPC는 SKOPC GNN-OPC 모듈의 직접적 선행 연구:
- **GNN-OPC 비교 기준**: SKOPC의 ResGNN 기반 OPC 모델과 GAN-OPC 직접 비교 가능
- **학습 데이터 파이프라인**: GAN-OPC의 타겟-마스크 쌍 생성 방식을 GNN 학습에 적용
- **손실 함수 설계**: 리소그래피 물리 손실 $\mathcal{L}_{litho}$을 `gnn_opc.py`에 통합
- **사전학습 전략**: ILT 공동 사전학습으로 GNN-OPC 수렴 가속 방법 참조

## 참고문헌 (핵심)
- Goodfellow et al., "Generative Adversarial Nets" (NeurIPS 2014)
- Ronneberger et al., "U-Net: Convolutional Networks for Biomedical Image Segmentation" (MICCAI 2015)
- Isola et al., "Image-to-Image Translation with Conditional Adversarial Networks" (CVPR 2017)
- Ma et al., "Rethinking the Open-Source Mask Optimisation" (ISPD 2020)

## 태그
`GAN-OPC`, `Generative Adversarial Network`, `Mask Optimization`, `OPC`, `ILT`, `Deep Learning`, `IEEE TCAD`, `2020`, `DAC 2018`, `U-Net`, `Lithography-guided`
