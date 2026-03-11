# LithoSim: A Large, Holistic Lithography Simulation Benchmark for AI-Driven Semiconductor Manufacturing

## 메타데이터
- **저자**: Hongquan He, 외 (CUHK, Bei Yu 연구그룹)
- **연도**: 2025
- **게재지/학회**: 39th Conference on Neural Information Processing Systems (NeurIPS 2025), Datasets and Benchmarks Track
- **DOI/URL**: https://openreview.net/forum?id=CtEocbcMyR; PDF: https://www.cse.cuhk.edu.hk/~byu/papers/C300-NeurIPS2025-LithoSim.pdf; HuggingFace: grandiflorum/LithoSim
- **인용수**: 신규 (2025년)

## 핵심 요약
AI 기반 반도체 제조를 위한 가장 포괄적인 리소그래피 시뮬레이션 벤치마크 LithoSim을 발표한 논문. 400만 개 이상의 고해상도 입출력 쌍(input-output pairs)과 엄밀한 물리적 대응 관계를 갖춘 데이터셋이다. 변경 가능한 광원 분포, OPC 변형을 포함한 메탈/via 마스크 토폴로지, 팹 현실적인 변동을 반영한 공정 윈도우를 체계적으로 통합한다. AI 성능과 리소그래피 충실도 모두를 포괄하는 도메인 특화 평가 지표로 통합 평가 프레임워크를 구축하며, 데이터/코드/사전학습 모델을 오픈소스로 공개한다.

## 주요 기여
- 400만 개 이상의 고해상도 입출력 쌍을 포함한 최대 규모 리소그래피 시뮬레이션 벤치마크
- 변경 가능한 광원 분포(광원 최적화 지원)
- OPC 변형 포함 메탈/via 마스크 토폴로지
- 팹 현실적 공정 윈도우 변동 포함
- AI 성능 + 리소그래피 충실도 통합 평가 프레임워크
- 데이터/코드/사전학습 모델 완전 오픈소스 공개

## 모델 아키텍처/수식
**LithoSim 데이터셋 구성:**
```
LithoSim
├── Total: 4,000,000+ input-output pairs
│
├── Mask Topology Variations:
│   ├── Metal layer (다양한 CD/pitch)
│   └── Via layer (고종횡비 패턴)
│
├── OPC Variants:
│   ├── Original layout (no OPC)
│   ├── Rule-based OPC
│   └── Model-based OPC + ILT
│
├── Source Variations (Optical):
│   ├── Conventional (σ=0.3~0.9)
│   ├── Annular (σ_in/σ_out)
│   ├── Dipole
│   └── Quadrupole
│
└── Process Window:
    ├── Focus: ±100nm variation
    ├── Dose: ±5% variation
    └── Nominal + best/worst case
```

**Ground Truth 생성:**
```
Mask → [Hopkins TCC model (엄밀 계산)] → Aerial Image
      → [Variable Threshold Resist Model] → Wafer Image
      → [Process Window Sampling] → PVBand
```
물리적 파라미터: ArF 193nm 이머전, NA=1.35

**평가 지표 (통합 프레임워크):**

AI 성능 지표:
```
Pixel Accuracy = (correct pixels) / (total pixels)
IoU = |predict ∩ GT| / |predict ∪ GT|
MSE = mean((I_pred - I_GT)²)
```

리소그래피 충실도 지표:
```
EPE = mean(|edge_pred - edge_GT|)  [nm]
PVBand = Area(Wafer_focus+ ⊕ Wafer_focus-)  [nm²]
NILS = (CD / |∂I/∂x|·I_r)|_{edge}  (이미지 로그 기울기)
```

**벤치마크 모델:**
- Physics-based: TorchLitho (기준)
- CNN: U-Net, ResNet
- FNO: Fourier Neural Operator
- Transformer: Vision Transformer (ViT)
- Hybrid: Dual-band NN, CFNO

**데이터셋 활용 시나리오:**
1. 리소그래피 시뮬레이션 가속 (maski → wafer image)
2. 역설계/마스크 최적화 (wafer image → mask)
3. 공정 윈도우 예측 (mask → PVBand)
4. 광원 최적화 (source + mask → wafer image)

## 모델 유형
- [x] 광학 모델 (Optical Model)
- [x] 레지스트 모델 (Resist Model)
- [x] ML/DL 모델
- [x] 하이브리드 모델

## OPC 툴 구현 관련성
LithoBench보다 더 크고 포괄적인 LithoSim은 SKOPC AI 모델 학습의 최고 품질 데이터셋. 400만 개 이상의 물리적으로 정확한 데이터로 SKOPC `skopc/modeling/gnn/` 모델을 학습하면 일반화 성능이 크게 향상. 광원 변형 포함으로 SMO(Source-Mask Optimization) 기능의 AI 가속에도 활용 가능. 공정 윈도우 데이터는 SKOPC `skopc/pwo/` 모듈 개선에 직접 활용. HuggingFace에서 접근 가능.

## 참고문헌 (핵심)
- Li, H. et al., "LithoBench," NeurIPS 2023
- Chen, G. et al., "Open-source differentiable lithography framework," arXiv:2409.15306 (2024)
- Wang, S. et al., "TorchResist," arXiv:2502.06838 (2025)
- Yang, H. et al., "Dual-band optics-inspired NN," DAC 2022
- Yang, H. et al., "CFNO+LGST," arXiv:2207.04056 (2022)

## 태그
`Model`, `OPC`, `Dataset`, `Benchmark`, `LithoSim`, `NeurIPS`, `LargeScale`, `ProcessWindow`, `SourceOptimization`, `SMO`, `OPC_Variants`, `HuggingFace`, `OpenSource`, `CUHK`
