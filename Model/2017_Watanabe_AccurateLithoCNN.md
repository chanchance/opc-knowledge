# Accurate Lithography Simulation Model Based on Convolutional Neural Networks

## 메타데이터
- **저자**: Yuki Watanabe, Taiki Kimura, Tetsuaki Matsunawa, Shigeki Nojima
- **연도**: 2017
- **게재지/학회**: SPIE Optical Microlithography XXX, Vol. 10147, paper 101470K
- **DOI/URL**: https://doi.org/10.1117/12.2257871
- **인용수**: 100+

## 핵심 요약
합성곱 신경망(CNN)을 리소그래피 시뮬레이션 모델에 적용한 선구적 논문. 기존 OPC 모델이 파라미터를 수동으로 선택해야 하는 한계를 CNN이 자동으로 적절한 모델 함수를 결정함으로써 극복한다. 실험 결과 CNN 모델은 기존 방법 대비 CD 예측 오차를 70% 감소시킨다. 이 논문은 딥러닝을 리소그래피 시뮬레이션에 본격 적용한 초기 연구 중 하나로, 이후 LithoGAN, DAMO 등의 연구를 촉발한 중요한 선구자 논문이다.

## 주요 기여
- CNN을 리소그래피 시뮬레이션 모델에 최초 본격 적용
- CD 예측 오차 70% 감소 (기존 방법 대비)
- 모델 함수 자동 선택: 인간 전문가 개입 최소화
- 마스크 이미지 → CD/웨이퍼 이미지 직접 매핑
- 이후 딥러닝 기반 리소그래피 시뮬레이션 연구의 기반

## 모델 아키텍처/수식
**기존 OPC 모델의 한계:**
```
기존 모델: CD = f(NILS, Ipeak, slope; a₁, a₂, ..., aₙ)
  - 모델 함수 선택: 전문가 경험 의존
  - 파라미터 수: 제한적
  - 복잡한 비선형 거동: 재현 어려움
```

**CNN 기반 리소그래피 시뮬레이션 모델:**

입력 특징 추출:
```
Input: 마스크 패턴 주변 이미지 타일 (N×N 픽셀)
       = aerial image patch around edge segment
```

CNN 구조:
```
[Conv1: 32 filters, 5×5] → ReLU → MaxPool
[Conv2: 64 filters, 3×3] → ReLU → MaxPool
[Conv3: 128 filters, 3×3] → ReLU
[Flatten]
[FC1: 256 units] → ReLU → Dropout(0.5)
[FC2: 64 units] → ReLU
[FC3: 1 unit] → CD prediction
```

**학습:**
```
Dataset: {(mask_patch_i, CD_meas,i)} from CD-SEM
Loss: L = Σᵢ (CD_pred,i - CD_meas,i)²
Optimizer: Adam (lr=0.001)
```

**예측:**
```
for each edge segment:
    patch = extract_aerial_image_patch(edge_position)
    CD_pred = CNN(patch)
    EPE = CD_pred - CD_target
    fragment_move = EPE / 2
```

**성능 비교:**
```
기존 VTR/LPM 모델: CD RMS error = 3.2nm
CNN 모델: CD RMS error = 0.96nm (70% 감소)
```

**왜 CNN이 효과적인가:**
1. 자동 특징 학습: 수동 특징 엔지니어링 불필요
2. 비선형 매핑: 복잡한 레지스트 거동 포착
3. 공간 정보 활용: 인접 패턴 영향 자동 학습
4. 다양한 패턴 일반화: 학습된 패턴 이외에도 적용

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 `skopc/modeling/gnn/` 모듈의 초기 선구자. CNN 기반 CD 예측은 GNN 기반 세그먼트 변위 예측의 전신이다. 이 논문의 aerial image patch 입력 방식은 SKOPC GNN의 특징 추출 단계에서 참조 가능. CD 예측 70% 오차 감소는 ML 기반 OPC 모델의 실용성을 최초로 입증한 결과로 역사적 중요성이 있다. SKOPC의 compact 레지스트 모델 대안으로 CNN 기반 모델 구현 시 이 논문의 아키텍처를 출발점으로 사용 가능.

## 참고문헌 (핵심)
- LeCun, Y. et al., "Gradient-based learning applied to document recognition," Proc. IEEE (1998)
- Cobb, N. and Zakhor, A., "Variable threshold resist model," SPIE 3679 (1999)
- Mack, C.A., "Lumped parameter model for CARs," SPIE 5377 (2004)
- Krizhevsky, A. et al., "ImageNet classification with deep CNN (AlexNet)," NeurIPS 2012
- Lin, Y. et al., "Data efficient lithography modeling with ResNet," ISPD 2018

## 태그
`Model`, `OPC`, `CNN`, `LithographySimulation`, `CDprediction`, `DeepLearning`, `AerialImage`, `SPIE`, `EarlyDeepLearning`, `70percentReduction`, `CompactModel`
