# Practical Inverse Mask Synthesis via Data-Efficient Physics-Informed Neural Networks (PINN) Model

## 메타데이터
- **저자**: Wang, K.-H., Fang, P.-H., Yu, P.-C. (NYCU, Taiwan)
- **연도**: 2025
- **게재지**: Proc. SPIE 13425, DTCO and Computational Patterning IV
- **DOI/URL**: https://doi.org/10.1117/12.3056774
- **인용수**: ~2

## 핵심 요약
역리소그래피(ILT: Inverse Lithography Technology)에 물리 정보 신경망(PINN)을 적용하여 계산 오버헤드를 대폭 줄이면서도 해 품질을 유지하는 실용적 역 마스크 합성 방법을 제안한다. U-Net 아키텍처에 리소그래피 물리 원리를 내장하고, 단/이중 Via 패턴 1800개만으로 학습하여 기존 ILT 대비 100× 이상 런타임 개선을 달성한다.

## 주요 기여
1. PINN 기반 ILT: U-Net + 리소그래피 물리 제약 내장으로 데이터 효율적 학습
2. 1800개 학습 패턴만으로 기존 ILT 품질의 92.5% 달성 (7.5% 이내 오차)
3. 추론 시 100× 이상 런타임 개선 (기존 ILT 대비)
4. 리소그래피 물리 손실 항으로 학습 데이터 부족 시 일반화 능력 향상
5. 단일 Via + 이중 Via 패턴에서 검증된 실용적 구현

## 모델 수식/아키텍처

**PINN ILT 모델:**
```
Input: target_pattern(x,y)  [웨이퍼 목표 패턴]
Model: U-Net + Physics constraints
Output: mask(x,y)          [최적 마스크]
```

**U-Net 아키텍처:**
```
Encoder: Conv → BN → ReLU (×4 scales, 64→512 channels)
Bottleneck: Conv → BN → ReLU
Decoder: ConvTranspose → BN → ReLU + Skip connections
Output: sigmoid → mask ∈ [0,1]
```

**물리 손실 항 (PINN):**
```
L_physics = ||I_sim(mask) - I_target||²
I_sim(mask) = Σ_k λ_k |φ_k * mask|²  (SOCS 기반 리소 시뮬레이션)
```

**전체 손실 함수:**
```
L_total = L_reconstruction + λ_phys · L_physics + λ_mfm · L_mask_fab
L_reconstruction = ||mask_pred - mask_ILT_ref||²  (레퍼런스 ILT와 비교)
L_mask_fab = ||∇mask||²  (마스크 복잡도 정규화)
```

**성능 비교:**
```
Traditional ILT: 1× (baseline)
PINN ILT (ours):
  - Runtime: 0.01×  (100× 빠름)
  - EPE RMS: ILT ×1.075  (7.5% 이내)
  - Training data: 1800 patterns (매우 적음)
```

## 모델 유형
- [x] 광학 모델 (SOCS 리소 시뮬레이션 내장)
- [ ] 레지스트 모델
- [x] ML/DL (U-Net PINN)
- [x] 하이브리드 (물리 제약 내장 신경망 ILT)

## OPC 툴 구현 관련성
- skopc ILT 모듈에 PINN 옵션 추가: 학습 후 초고속 마스크 합성
- 학습 데이터: 기존 ILT 결과 1800개로 충분 (데이터 효율적)
- 추론 파이프라인: target_pattern → U-Net → mask (단일 순전파)
- 제한: 학습 분포 내 패턴에 한정 → 새로운 패턴 유형에는 재학습 필요
- Ju et al. (2024) PINN M3D와 상보적: 마스크 합성 + 마스크 EM 시뮬레이션

## 참고문헌
- Raissi, M. et al., "Physics-informed neural networks" (2019, JCP)
- Ju, X. et al., "3D mask simulation using PINN" (2024)
- Yang, Y. et al., "GPU-accelerated ILT for curvilinear mask" (2024)

## 태그
`Model`, `SPIE`, `PINN`, `ILT`, `UNet`, `PhysicsInformed`, `DataEfficient`, `MaskSynthesis`, `2025`
