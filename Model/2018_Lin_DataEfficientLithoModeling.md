# Data Efficient Lithography Modeling with Residual Neural Networks and Transfer Learning

## 메타데이터
- **저자**: Yibo Lin, Yuki Watanabe, Taiki Kimura, Tetsuaki Matsunawa, Shigeki Nojima, Meng Li, David Z. Pan
- **연도**: 2018
- **게재지/학회**: ACM International Symposium on Physical Design (ISPD 2018)
- **DOI/URL**: https://doi.org/10.1145/3177540.3178242; arXiv:1807.03257
- **인용수**: 120+

## 핵심 요약
리소그래피 모델링에서 데이터 효율성 문제를 해결하기 위해 잔차 신경망(ResNet)과 전이 학습(Transfer Learning)을 결합한 방법론을 제안한 논문. 기존 CNN 기반 학습 방법들은 데이터를 매우 많이 필요로 하고, 특정 리소그래피 구성에서 수집한 데이터는 오직 하나의 모델 학습에만 유효한 낮은 데이터 효율성 문제를 가진다. ResNet이 깊은 신경망에서 CNN보다 더 나은 수렴성을 보이며, 전이 학습과 결합 시 훨씬 적은 데이터로 높은 성능을 달성함을 입증한다.

## 주요 기여
- 리소그래피 모델링에서의 데이터 효율성 문제 정의 및 해결
- ResNet이 리소그래피 모델링에서 CNN보다 우수한 수렴성 입증
- 전이 학습을 통한 공정 노드 간 모델 재사용 가능성 시연
- 능동 데이터 선택(active data selection) 전략으로 데이터 수집 효율화
- 소량 데이터로 새로운 공정 구성에 빠르게 적응하는 few-shot 학습 프레임워크

## 모델 아키텍처/수식
**잔차 신경망(ResNet) 기반 리소그래피 모델:**

기본 잔차 블록:
```
y = F(x, {Wᵢ}) + x

F(x) = W₂ · σ(BN(W₁ · x))   (2-layer residual)
```
σ: ReLU 활성화, BN: Batch Normalization

**리소그래피 모델링 네트워크 구조:**
```
Input: 마스크 타일 (binary, N×N)
       ↓
[Stem Conv 7×7, stride 2]
       ↓
[ResBlock × 4] (채널: 64→128→256→512)
       ↓
[Global Average Pooling]
       ↓
[FC Layer] → 웨이퍼 CD 또는 이미지 예측
```

**전이 학습 전략:**
```
Source Task: 기준 공정 (예: ArF 193nm, NA=1.35)에서 학습
Target Task: 새로운 공정 (예: EUV 13.5nm)에서 적응

단계:
1. Source 데이터로 전체 모델 학습: W_source
2. Target 데이터 일부로 미세 조정(fine-tuning):
   - 하위 레이어 고정 (feature extractor 재사용)
   - 상위 레이어 + FC만 재학습: W_target
```

**능동 데이터 선택 (Active Data Selection):**
```
D_labeled: 이미 레이블된 데이터 (CD-SEM 측정 완료)
D_unlabeled: 레이블 미부여 데이터

선택 기준: 불확실성(uncertainty) 최대화
x* = argmax_{x∈D_unlabeled} Var[f_θ(x)]
```
Dropout을 이용한 Monte Carlo 불확실성 추정:
```
Var[f_θ(x)] ≈ (1/T) Σₜ [f_θₜ(x) - f̄(x)]²
```

**손실 함수:**
```
L = Σᵢ ||CD_pred,i - CD_measured,i||² + λ · ||W||²
```

**성능 (비교 실험):**
| 방법 | 데이터 500개 EPE | 데이터 100개 EPE |
|------|-----------------|-----------------|
| CNN | 3.2nm | 5.8nm |
| ResNet | 2.1nm | 3.9nm |
| ResNet+TL | 1.8nm | 2.5nm |

## 모델 유형
- [ ] 광학 모델 (Optical Model)
- [ ] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
SKOPC의 GNN-OPC 모델 학습 효율화에 직접 적용 가능. 반도체 공정 변경 시(예: ArF→EUV, 28nm→7nm) 전이 학습으로 CD-SEM 데이터 수집 비용을 최소화하면서 모델을 빠르게 적응시키는 방법을 제공. 능동 데이터 선택을 SKOPC의 보정(calibration) 패턴 자동 선택에 통합하면 측정 효율을 높일 수 있다. `recipes/example_euv.yaml` 시나리오 전환 시 이 전이 학습 전략 활용 권장.

## 참고문헌 (핵심)
- He, K. et al., "Deep residual learning for image recognition (ResNet)," CVPR 2016
- Pan, S.J. and Yang, Q., "A survey on transfer learning," IEEE Trans. Knowledge Data Eng. (2010)
- Ye, C. et al., "LithoGAN," DAC 2019
- Settles, B., "Active learning literature survey," Univ. Wisconsin-Madison (2009)

## 태그
`Model`, `OPC`, `ResNet`, `TransferLearning`, `DataEfficiency`, `LithographyModeling`, `ActiveLearning`, `DeepLearning`, `ISPD`, `FewShot`, `CDprediction`
