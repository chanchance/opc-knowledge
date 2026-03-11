# Using Machine Learning Etch Models in OPC and ILT Correction

## 메타데이터
- **저자**: Hooker, K., Zavyalova, L., Huang, S., Chen, L.-J. (Synopsys)
- **연도**: 2021
- **게재지**: Proc. SPIE 11614, Optical and EUV Nanolithography XXXIV
- **DOI/URL**: https://doi.org/10.1117/12.2587225
- **인용수**: ~25

## 핵심 요약
기존 규칙 기반 에칭 근접 효과 처리 방식을 머신러닝(ML) 에칭 모델로 대체하여 OPC 및 ILT 보정 플로우에서의 에칭 모델 정확도와 처리 속도를 동시에 향상시킨다. ML 에칭 모델이 전통적인 항(term) 기반 모델이 포착하기 어려운 복잡한 비선형 에칭 거동을 학습하고, 전체 칩 마스크 합성 플로우에서 실용적으로 적용 가능함을 실증한다.

## 주요 기여
1. 신경망 기반 ML 에칭 모델의 OPC/ILT 통합 실용적 구현
2. 규칙 기반 에칭 모델 대비 비선형 에칭 거동 포착 능력 향상
3. 처리 속도(TAT) 유지하면서 에칭 모델 정확도 개선
4. ILT 마스크 합성 플로우에서 ML 에칭 모델 통합 방법론
5. 대규모 SEM 메트롤로지 데이터 활용 ML 에칭 모델 학습 절차

## 모델 수식/아키텍처

**ML 에칭 모델 구조 (신경망):**
```
Input features:
  - CD_litho (리소 CD)
  - local_density(r₁), local_density(r₂), ...  (다중 반경 밀도)
  - pitch, orientation, aspect_ratio
  - CD_neighbors (인접 패턴 CD)
  - image_slope (공중상 기울기)

Hidden layers: MLP 3-4 layers (128-256 units, ReLU/GELU)
Output: etch_bias = CD_etch - CD_litho
```

**학습 데이터 생성:**
```
Training pairs: (layout_context_i, etch_bias_meas_i)
etch_bias_meas = CD_SEM_post_etch - CD_SEM_post_litho
N_training: 수천~수만 개 게이지
```

**학습 목적함수:**
```
L = Σ_i (etch_bias_pred_i - etch_bias_meas_i)² + λ·||W||²
```

**OPC 통합:**
```
CD_litho_target = CD_wafer_target - ML_etch_model(layout_context)
mask = Litho_OPC(CD_litho_target)
```

**ILT 통합:**
```
Cost_ILT = ||I_sim(mask) - I_target||²
         + λ_etch · ||ML_etch_model(mask_context) - etch_target||²
```

**성능 비교:**
```
RMS_term_based: ~1.5nm
RMS_ML: ~0.9nm  (40% 향상)
TAT_ML / TAT_term: ~1.1×  (10% 증가, 허용 범위)
```

## 모델 유형
- [ ] 광학 모델
- [ ] 레지스트 모델
- [x] ML/DL (신경망 에칭 모델)
- [x] 하이브리드 (ML 에칭 + 물리 리소 모델)

## OPC 툴 구현 관련성
- skopc ML 에칭 모델 모듈: 신경망 기반 etch bias 예측
- 학습 데이터: 리소 후 + 에칭 후 CD-SEM 동시 측정 필요
- 특성 공학: 다중 반경 밀도 맵 계산이 핵심 전처리
- ILT 통합: 에칭 비용 항을 ILT 목적함수에 미분 가능 형태로 추가
- Synopsys Proteus Etch Modeling의 ML 옵션 이론적 기반

## 참고문헌
- Lafferty, N. et al., "Etch kernels for etch bias prediction" (2018)
- Shang, S. et al., "Etch proximity correction by retargeting" (2007)
- Sato, T. et al., "Deep-learning based etch model" (2022)

## 태그
`Model`, `SPIE`, `EtchModel`, `MachineLearning`, `NeuralNetwork`, `OPC`, `ILT`, `EtchBias`, `2021`
